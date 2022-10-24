from PIL import Image
import random

img2 = Image.open('22.bmp')

width, height = img2.size #ширина и высота
pix = img2.load()

for x in range(0, width-1):
    if x-1 > 0 and x < width:
        for y in range(0, height-1):
            if y-1 > 0 and y < height: #для каждого пикселя и для 8 вокруг него берем среднее значение этих цветов и сохраняем в переменные
                l1 = (0.3 * pix[x-1, y-1][0]) + (0.59 * pix[x-1, y-1][1]) + (0.11 * pix[x-1,y-1][2]) #l=0.3*R+0.59*G=0.11*B по формуле RGB яркости
                l2 = (0.3 * pix[x - 1, y][0]) + (0.59 * pix[x - 1, y][1]) + (0.11 * pix[x - 1, y][2])
                l3 = (0.3 * pix[x - 1, y + 1][0]) + (0.59 * pix[x - 1, y + 1][1]) + (0.11 * pix[x - 1, y + 1][2])
                l4 = (0.3 * pix[x, y - 1][0]) + (0.59 * pix[x, y - 1][1]) + (0.11 * pix[x, y - 1][2])
                l5 = (0.3 * pix[x, y][0]) + (0.59 * pix[x, y][1]) + (0.11 * pix[x, y][2])
                l6 = (0.3 * pix[x, y + 1][0]) + (0.59 * pix[x, y + 1][1]) + (0.11 * pix[x, y + 1][2])
                l7 = (0.3 * pix[x + 1, y - 1][0]) + (0.59 * pix[x + 1, y - 1][1]) + (0.11 * pix[x + 1, y - 1][2])
                l8 = (0.3 * pix[x + 1, y][0]) + (0.59 * pix[x + 1, y][1]) + (0.11 * pix[x + 1, y][2])
                l9 = (0.3 * pix[x + 1, y + 1][0]) + (0.59 * pix[x + 1, y + 1][1]) + (0.11 * pix[x + 1, y + 1][2])
                lll = (l1+l2+l3+l4+l5+l6+l7+l8+l9)/8 #среднее арифметическое этих значений
                if l5 >= lll: #если средний оттенок пикселей больше(т.е.хуже), то считаем его шумом
                    img2.putpixel((x, y), (int(pix[x, y][0]*lll/l5),int(pix[x,y][1]*lll/l5),int(pix[x,y][2]*lll/l5))) #меняем на средний по цвету среди окружающих
img2.save('22.jpg')
img2.show()
