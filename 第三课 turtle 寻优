import argparse
import inspect
import random
import pickle
import turtle


def draw_bag():
  bag = turtle.Turtle()
  bag.pen(pencolor='brown', pensize=5)
  bag.penup()
  bag.goto(-35, 35)
  bag.pendown()
  bag.right(90)
  bag.forward(70)
  bag.left(90)
  bag.forward(70)
  bag.left(90)
  bag.forward(70)
  bag.hideturtle()

def draw_line():   #定义几种常见的行走策略，画直线
  angle = 0
  step = 5
  t = turtle.Turtle()
  while not escaped(t.position()):
    t.left(angle)
    t.forward(step)

def draw_square(t, size):  #定义几种常见的行走策略，画正方形
  L = []
  for i in range(4):
    t.forward(size)
    t.left(90)
    store_position_data(L, t)
  return L

def draw_squares(number):  #定义几种常见的行走策略，画正方形
  t = turtle.Turtle()
  L = []
  for i in range(1, number + 1):
    t.penup()
    t.goto(-i, -i)
    t.pendown()
    L.extend(draw_square(t, i * 2))
  return L

def draw_triangles(number):  #定义几种常见的行走策略，画三角形
  t = turtle.Turtle()
  for i in range(1, number):
    t.forward(i*10)
    t.right(120)

def escaped(position):    # 超出边缘则逃脱成功
  x = int(position[0])
  y = int(position[1])
  return x < -35 or x > 35 or y < -35 or y > 35

def store_position_data(L, t):  # 存储位置信息，
  position = t.position()
  L.append([position[0], position[1], escaped(position)])

def draw_spirals_until_escaped():   # 画螺旋形 直到逃离
  t = turtle.Turtle()
  t.penup()
  t.left(random.randint(0, 360))   #引入随机变量 角度随机
  t.pendown()

  i = 0
  turn = 360/random.randint(1, 10)
  L = []
  store_position_data(L, t)
  while not escaped(t.position()):
    i += 1
    t.forward(i*5)
    t.right(turn) 
    store_position_data(L, t)
  return L


def draw_squares_until_escaped(n):   # 画正方形 直到逃离
  t = turtle.Turtle()
  L = draw_squares(n) 
  with open("data_square", "wb") as f:
    pickle.dump(L, f)     #序列化对象，将对象data_square 保存到文件wb中去

def draw_random_spirangles():   # 画随机可变矢量
  L = []
  for i in range (10):
    L.extend(draw_spirals_until_escaped())

  with open("data_rand", "wb") as f:
    pickle.dump(L, f)

if __name__ == '__main__':
  fns = {"line": draw_line,
        "squares": draw_squares_until_escaped,
        "triangles": draw_triangles,
        "spirangles" : draw_random_spirangles}

  parser = argparse.ArgumentParser()
  parser.add_argument("-f", "--function", choices = fns,help="One of " + ', '.join(fns.keys()))
  parser.add_argument("-n", "--number", default = 50,type=int, help="How many?")
  args = parser.parse_args()


  try:
    f = fns[args.function]
    turtle.setworldcoordinates(-70., -70., 70., 70.)
    draw_bag()
    turtle.hideturtle()
    if len(inspect.getargspec(f).args)==1:
      f(args.number)
    else:
      f()
    turtle.mainloop()
  except KeyError:
    parser.print_help()
