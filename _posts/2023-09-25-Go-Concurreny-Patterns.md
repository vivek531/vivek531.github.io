---
layout: post
title: "Python packages"
date: 2023-09-25
---

To understand concurreny in go, there are some primitives that we need to understand first.

**1. goroutines**
We can run functions concurrently by just adding go keyword in front of the function invocation.

```
func main() {
    someFunc()
    fmt.Println("hi")
}

func main() {
    go someFunc() // just adding go keyword makes this function run concurrently.
    fmt.Println("hi")
}
```

**2. Channels**
So far, our goroutines can go off and do their thing but they do not coordinate with other goroutines. That is where the channel comes in. It is a shared data structure in memory where goroutines can write data to and read data from.

Something like this. Here, the goroutine writes data to channel and main routine reads data from the channel.

```
func main() {
    myChannel := make(chan string)
    go someFunc() {
        myChannel <- "data"
    } ()

    msg := <- myChannel
    fmt.Println(msg)
}
```

**3. select**
For now, we have just one channel that our main function reads data from. But, in real life scenarios, we might have multiple channels and we might want to read data from them. Thats where select statement come in.

Like so, we have two channels and we write data to both channels. At the end we wait for one of the channels to write the data so we can read and continue. If both channels are ready with data, then main will read one at random.

```
func main() {
    myChannel := make(chan string)
    go someFunc() {
        myChannel <- "data"
    } ()
    otherChannel := make(chan string)
    go someFunc() {
        myChannel <- "cow"
    } ()

    select {
        case msg := <- myChannel:
            fmt.Println(msg)
        case msgFromOtherChannel := <- otherChannel:
            fmt.Println(msgFromOtherChannel)
    }
}
```

Now, we have looked at the 3 primitives that we essential for concurreny in go. Now we will look at three most important concurrency patterns

**1. for select pattern**

Before we get into for select, the channels we create can be of two types. Buffered channels and unbuffered channels. When we specify the capacity of the channel in the constructor, we get a buffered channel and when capacity is zeo or undefinded we get unbuffered channel.

One more difference between buffered and unbuffered channels is that buffered channel is asynchrous and unbuffered channel is synchronous.

Now, onto the for select! This concept is understood better with code. In one code, we are adding data to a channel inside a for loop. And in the other code, we create a never ending goroutine.

```
func main() {
    myChannel := make(chan string , 3)
    chars := []string{'a', 'b', 'c'}

    for _, char := range chars {
        select {
            case myChannel <- char
        }
    }

    close(myChannel)
    for result := range myChannel {
        fmt.Println(result)
    }
}

```

Code where goroutine is working indefinitely
```
func main() {

    go someWork() {
        for {
            select {
                default:
                    fmt.Println("Doing work")
            }
        }
    } ()
}
```

**2. done channel**

Next challenge for us to solve is how the main function can stop the indefinitely running goroutine in the last section. We are going to use done channel for that. The goroutine will accept done channel as a read only channel as it can not write anything to it. Only the main function will write to it when it wants to stop all the goroutines.

```
dowork(done <-chan bool) {
    for {
        select {
            case <- done:
                return
            default:
                fmt.Println("Doing work")
        }
    }
}

func main() {
    done := make(chan, bool)
    go dowork(done)

    time.sleep(time.seconds*3)
    close(done)
}
```
