# Teaching-HEIGVD-AMT-2019-Labo-02
## Introduction and objectives

In the first lab, we have made our first experiments with Java EE application servers. By now, we know how to run app servers both locally and in Docker. We know how to deploy applications in a them. Last but not least, we have an integrated development environment, which allows us to debug applications running in our servers.

In the second lab, we continue with basic experiments that will allow us to get more familiar with Java EE development. The goal is to make sure that everyone is able to replicate the experiments shown during the lecture. In particular, we want to make sure that everyone is able to create JMeter tests and to observe the behavior of the system in different situations.

There is still nothing to hand out at the end of the lab. This is preparation work for the projects, which we will start once we have acquired the basic knowledge and skills. There is a list of things that you have to make sure that you fully understand at the end of the lab:

## Objective 1: replicate the ServletCounter experiment

During the lecture, we have seen that it is possible to reproduce a concurrency bug in a Servlet, by generating concurrent requests with JMeter. The experiment is documented in the AMT Book and in a series of 4 webcasts.

This should be the starting point for this lab session. Make sure that you are able to reproduce the experiment. You have to be able to prove that the bug exists. You also have to show that after implementing the bug fix, the error is not visible anymore.

## Objective 2: design an experiment to study the behavior of Stateless Session Beans

During the lecture, I have mentioned that Stateless Session Beans (a kind of EJB) have a different behavior than servlets from a concurrency point of view. I have hinted that the application server creates multiple instances of the session bean, and that only one thread can be executed on a given instance at any time.

Do you believe me? I don't want you to blindly trust me. You have to design an experiment to observe if that seems to be the case or not. Running an experiment is done in 3 steps. Firstly, you will need to write some code and formulate an hypothesis (doing this, you will learn how to write your first EJB and to call it from a servlet... viva la dependency injection). Secondly, you will need to create a test plan with JMeter and run it. Last and most importantly, you will need to read, analyze and interpret the results. Is the outcome of the JMeter test invalidating or validating your hypothesis? You need to be able to write this down and to explain it. Take the time to do it, it will save you time when time comes to write your project report.

## Objective 3: design an experiment to study the impact of using the HTTP session in a servlet

*This is an advanced step. If the first 2 steps were easy for you, you will have something a bit more challenging to do. If you don't manage to finish this last step, do not worry: we will come back to the topic during the lecture (but after that, you will need to be able to explain it!).*

During the lecture, we have seen how to pass information between the controller and the view, using the `request.setAttribute`method. There is another class exposing a `setAttribute`method: `HttpSession`. You need to learn how to use it, because sooner or	 later, you will need it (as soon as you implement a user login feature).

Behind the scenes, the application server allocates memory for every HTTP session (that is, for every user that is supposed to be still "active"). You will see that it is easy to use and quite practical. But with great power comes great responsibility... Imagine that you start to stuff lots of information in the session (maybe an image, a list of 10'000 products, etc.). What happens if you then have 200, 2'000 or 20'000 active users? How long is your app server going to survive?

How would you design and run an experiment to study the behavior of the app server in this context? Here are a couple of points that you should consider:

* Think of a strategy to generate the "heavy" data to be stored in the session (byte arrays are one way to go)
* Make sure that your JMeter handles cookies correctly. You will need to setup a cookie store. Watch carefully the recorded responses, to be sure that you are *really* reusing an existing session when you send the follow-up requests.
* Think of a strategy to observe your app server, and in particular its resource consumption. Hint: have a look at JConsole, a tool that is bundled with the JDK and that will give you plenty of information about memory usage, threading, etc.