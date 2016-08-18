# Why do unit tests

- can act as and or repalce documentation, thinking about:
 - behaviour driven tests

- test driven development might be easier and faster development:

 - e. g. the never tested exception which fails cause never tested.
This actually might save time considering the whole game because searching
these small issues a view weeks / month later might take more time than
just testing it now.

 - in some cases automated tests run faster than reloading the webpage or
restarting the server etc.

- improve developer skills and improve code quality because
fast and good test cases requires to think more decoupled and component like

- automated tests most like are comming with automated test data. Which save tons of time
if you dont have to create test data by hand, but always can create it automatically

- easier introduction for new developers

- saver, faster introduction of new features

- saver, faster refactoring, performance opting


- Continous manual tests ARE error prone due to human misstakes caused by "boring repeating work". Quickly we start to assume that we thought of all (but in most cases we are damn wrong)

- JavaScript: The nature of the language, its dynamism, makes it easy to introduce errors.

- in some cases it can make the difference between making any change at all, or holding back out of fear of breaking something that seems to be working well enough

- Tdd acts as first feedback for the programmmer during writing the programm. By recognising that writing tests for a particular piece of code is very hard you might realise that it could be done better and you start to change codes architecture during its development (whichis the cheapest moment at all)