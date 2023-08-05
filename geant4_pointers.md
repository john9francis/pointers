# Geant4's use of pointers

[home](README.md)


# pointers in Geant4
It's cool to understand pointers and all, but what's the purpose of using them? To find out, let's disect the pointer use in a more complicated program, Geant4. 

Geant4 is a physics simulation toolkit written in C++. It uses pointers a lot, which saves valuable computational time. 

We are going to dissect the use of pointers in a Geant4 application and see what would happen if we didn't use pointers. 
