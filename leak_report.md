# Leak report

Inside of the `is_clean` method, there is a string (character array) `cleaned` that is created and then compared to the provided string (charcter array) argument. However, `is_clean` then reaches its return statement. This causes the memory used by `cleaned` to become unusable. The approach I will take to fix this leak is to call free() after the comparison, but before the return.

WARNING: In the case of the provided string (character array) being all spaces, the `cleaned` variable does not need to be freed, since the strip() method will remove all of the spaces and replace them with \0. In order to avoid an error, we need an additional if statement to first check that the length of cleaned is not equal to 0 before attempting to free it.
