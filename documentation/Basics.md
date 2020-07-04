# Basics
## Good Sources
Most of the content of the original nreal Engine Wiki was migrated to the new community hosted Wiki. Regarding Multi Threading, one can find many useful tutorials by Rama.
- [Unreal Engine Community Wiki](https://www.ue4community.wiki/Unreal_Engine_Community_Wiki)

Another good source of tutorials ist the website of Orfeas Eleftheriou. There are also good tutorials regarding multi threading
- [Orfeas Eleftheriou](www.orfeasel.com/blog/)

## UPROPERTIES

[Unreal Documentation: Property & Metadata Specifiers](https://docs.unrealengine.com/en-US/Programming/UnrealArchitecture/Reference/Properties/Specifiers/index.html)

## Delegates
When working with Delegates, you must not forget to only bind them to functions with the UFUNCTION tag. Otherwise they won't work correctly!

[Creating and Using Delegates C++ and Accessing them in Blueprints.](https://forums.unrealengine.com/community/community-content-tools-and-tutorials/13915-tutorial-creating-and-using-delegates-c-and-accessing-them-in-blueprints)  
[Unreal Documentation: Delegates](https://docs.unrealengine.com/en-US/Programming/UnrealArchitecture/Delegates/index.html)

### Binding via Blueprints
when you want to bind blueprint events to a c++ delegate, you will have to use a dynamic delegate. It is not possible to usa a multicast delegate. AS a workaround, you can create a TArray of Delegates, to use for the binding.  
1. declare the delegate ```DECLARE_DYNAMIC_DELEGATE(FMyDelegate);```
2. declare a local variable to store the bound events 
    ``` cpp
    UPROPERTY()
    TArray<FMyDelegate> MyDelegateArray;
    ```
3. now you can bind events to the delegate array
    ``` cpp
    void MyClass::BindToDelegate(const FMyDelegate Event) {
	    MyDelegateArray.Add(Event); // bind
        MyDelegateArray.Remove(Event); // unbind
    }
    ```
4. to call the events you can loop over the array
    ``` cpp
    for (FMyDelegate Element : MyDelegateArray) {
		Element.ExecuteIfBound();
	}
    ```

## Interfaces

[Unreal Engine C++ Fundamentals – Interfaces!](http://jollymonsterstudio.com/2019/05/30/unreal-engine-c-fundamentals-interfaces/)  
[UE4 – Declaring and using interfaces in C++](https://isaratech.com/ue4-declaring-and-using-interfaces-in-c/)  
[Unreal Documentation: Interfaces](https://docs.unrealengine.com/en-US/Programming/UnrealArchitecture/Reference/Interfaces/index.html)