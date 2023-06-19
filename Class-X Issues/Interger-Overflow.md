# Integer Overflow Occurs In Calculation Done By Server
```bash
Let’s say Item A is 10$ each and Item B is 80$ each.
I ordered 9223372036854775808 of item A.

Upon submitting, the quantity becomes -9223372036854775808, proving the existence of the integer overflow bug.

I ordered again 9223372036854775800 of item A so I will have -8 items of Item A in total.

Now, my cart total is -80$

I ordered 1 item of Item B (80$)

Now, my cart total is $0.00
```
