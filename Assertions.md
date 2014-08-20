Lots of times, we want to make sure certain conditions in the code, such as range bounds on variables: non-negative indices, matching vector/matrix sizes, parameters in [0,1], etc. There are two different cases to check:

1.  User specified inputs. I.e. when users have the power to break these conditions
2. Internal checks. I.e. when the user is not able to break the condition, but you want to make sure that things are working in your code

First of all, number 2. is not necessary at all. You should rather write proper unit-tests for your code than being lazy and relying on assertions to check whether things are working correctly.

For the other one: Although we have an ```ASSERT``` macro, please try to avoid it where possible. Imagine there is code like
```
void foo(index_t i)
{
...
ASSERT(i>=0);
...
}
```
All the user will get when running Shogun is an assertion error. If he is brave and turns on printing line and file of the error, the information is very sparse, resulting in frustration