Lots of times, we want to make sure certain conditions in the code, such as range bounds on variables: non-negative indices, matching vector/matrix sizes, parameters in [0,1], etc. There are two different cases to check:

1.  User specified inputs. I.e. when users have the power to break these conditions
2. Internal checks. I.e. when the user is not able to break the condition, but you want to make sure that things are working in your code

First of all, number 2. is not necessary at all. It is _just for your convenience_. You should rather write **proper [unit-tests](Unit-Testing)** for your code than being lazy and relying on assertions to check whether things are working correctly.

For the other one: Although we have an ```ASSERT``` macro, please try to avoid it where possible. Imagine there is code like
```
void foo(index_t i)
{
...
ASSERT(i>=0);
...
}
```
All the user will get when running Shogun is an assertion error. If he is brave and turns on printing line and file of the error, the information is very sparse, resulting in frustration.

Instead, use the ```REQUIRE``` macro, and give **proper error messages**, which means information of what is wrong, and in particular _how it differs from what was expected_. Example
```
void foo(index_t i, SGVector<index_t> inds)
{
...
REQUIRE(i>=0, "Provided index (%d) must be greater than 0\n", i);
...
REQUIRE(inds.vlen==this->bar.vlen, "Provided index vector length (%d) must match the length of internal vector (%d).\n", inds.vlen, this->bar.vlen);
}
```

Finally
* Use **proper** English (Start with capital letters, write sentences)
* Don't forget ```\n``` at the end.
* Make sure that you **don't cause segfaults**

```
void foo(SGVector<index_t> inds)
{
...
// First check makes sure that second check does not segfault
REQUIRE(inds.vlen>=1, "Length of provided vector (%d) must be at least 1.\n", inds.vlen);
REQUIRE(inds[0]>0, "First element of provided vector (%d) must be greater than 0.\n", inds[0]);
}
```

```
void foo(CKernel* kernel)
{
...
// First check makes sure that second check does not segfault
REQUIRE(kernel, "No kernel provided.\n");
REQUIRE(kernel->get_width()>=1, "Provided kernel width (%f) must be greater than 1.0.\n", kernel->get_width());
}
```