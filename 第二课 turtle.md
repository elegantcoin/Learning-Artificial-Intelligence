```python
#  Escape/hello_turtle.py
import turtle

def draw_bag():
  turtle.shape('turtle') 
  turtle.pen(pencolor='red', pensize=5)
  turtle.penup()
  turtle.goto(-35, 35) 
  turtle.pendown()
  turtle.right(90)
  turtle.forward(70) 
  turtle.left(90)
  for i in range(14):
    for j in range(2):
        turtle.forward(70-5*i) 
        turtle.left(90)
     

if __name__ == '__main__':
  turtle.setworldcoordinates(-70., -70., 70., 70.) 
  draw_bag()
  turtle.mainloop() 
```
