# texbox
Copie o texto abaixo para um ambiente virtual Python (pycharm) e execute

import pygame
import time
pygame.init()
display =pygame.display.set_mode((700, 1000)) 
def label(win, text='', font1=24,posx=400,posy=400):
	font = pygame.font.SysFont("DejaVuSans", font1)
	txt = font.render(text, 1, (0, 0, 0))
	win.blit(txt,(posx, posy))
class Input:
	def __init__(self,color, x, y, l, a, font=24):
		self.color=color
		self.c1=color
		self.x=x
		self.y=y
		self.a=a
		self.l=l
		self.text='' 
		self.font=font
		self.cx=0
		self.cursor_pos=0
		self.cursor='|'
		self.t=False
		self.l1=l
		self.x1=x
		self.act=0
	def draw(self,win,pos=''):
		t=self.t
		vl=0
		text=''
		if self.t==True and self.cursor not in self.text :
			t=list(self.text)
			t.insert(self.cursor_pos,self.cursor)
			self.text=str(''.join(t))
		if self.t==False and '|' in self.text and self.cursor_pos >-1 and self.cursor==self.text[self.cursor_pos]:
			t=list(self.text)
			t.pop(self.cursor_pos)
			self.text=str(''.join(t))
		if self.text !='':
			font = pygame.font.SysFont("DejaVuSans", self.font)
			text = font.render(self.text, 1, self.color)
			self.l=text.get_width()
		else:
			self.l=self.l1
		if self.text[-4:len(wb.text)]=='§g7§' or self.text[-5:(len(wb.text)-1)]=='§g7§' and (self.cursor_pos+1)==len(self.text) :
			self.color=(0,255,0)
		else:
			self.color=self.c1
		self.a=self.font+self.font/2
		pygame.draw.rect(win,(0,0,0), (self.x1, self.y,self.l1, self.a))
	#	pygame.draw.rect(win, self.color, (self.x1, self.y,self.l1, self.a))
		if text!='':
			win.blit(text, (self.x, self.y))
		pygame.draw.rect(win, (255,255,255), (0, self.y,self.x1, self.a))
		pygame.draw.rect(win, (255,255,255), ((self.x1+self.l1), self.y,self.l, self.a))
	def touch(self,pos):
				if pos[0] > self.x1 and pos[0]< self.x1 + self.l1:
					if pos[1] > self.y and pos[1]< self.y + self.a:
						return True
					return False
	def touch1(self,pos):
				if pos[0] > self.x1 and pos[0]< self.x1 + 20 :
					if pos[1] > self.y and pos[1]< self.y + self.a:
						return True
					return False
	def touch2(self,pos):
		if pos[0] <self.l1+self.x1 and pos[0]> (self.x1+self.l1)-20:
					if pos[1] > self.y and pos[1]< self.y + self.a:
						return True
					return False
	
	def edtext(self,ev):
		if ev.type==pygame.TEXTINPUT and not self.act==1:
			text=list(self.text)
			text.insert(self.cursor_pos,ev.text)
			self.text=''.join(text)
			if not self.cursor_pos>len(self.text):
				self.cursor_pos+=1
			elif self.cursor_pos>len(self.text):
				self.cursor_pos=len(self.text)
			font = pygame.font.SysFont("DejaVuSans", self.font)
			txt1= font.render(self.text, 1, (255, 0, 0))
			pl=(txt1.get_width())/len(self.text)
			l=-self.l+txt1.get_width()
			self.l=txt1.get_width() 
			pl=((self.l-30)/len(self.text))
			tcp=self.text[0:self.cursor_pos+1]
			fnt = pygame.font.SysFont("DejaVuSans", self.font)
			tcp= fnt.render(tcp,1, (255, 0, 0))
			cp=tcp.get_width()+self.x
			cp1=tcp.get_width()
			if self.l>=self.l1 and self.cursor_pos+1==len(self.text) :
				self.x=((self.l1+self.x1)-self.l)
			elif self.l<self.l1:
				self.x=self.x1
			elif not self.cursor_pos==len(self.text) and cp>=(self.x1+self.l1): 
				self.x=((self.x1+self.l1)-(cp1))
					
		if ev.type==pygame.KEYUP and not self.act==1:
			if ev.key==8:
				if len(self.text)>0 and self.cursor_pos>0:
					t=list(self.text)
					t.pop(self.cursor_pos-1)
					self.text=str(''.join(t))
					if self.cursor_pos>-1:
						self.cursor_pos-=1
						font = pygame.font.SysFont("DejaVuSans", self.font)
						txt2= font.render(self.text, 1, (255, 0, 0))
						pl=(txt2.get_width())/len(self.text)
						l=-self.l+txt2.get_width()
						self.l=txt2.get_width() 
						if self.l<=txt2.get_width() and  self.l>=self.l1 and  self.x+self.l >self.x1+self.l1 and self.cursor_pos+1==len(self.text) :
							self.x=((self.l1+self.x1)-self.l)
						elif self.l<self.l1:
							self.x=self.x1
						if self.l>self.l1 and not self.cursor_pos==len(self.text) :
							self.x=self.x-l
						
	def change_cursor_pos(self,pos,pos1):
		if self.touch(pos) and len(self.text)>1:
			if '|' in self.text:
				t=list(self.text)
				t.pop(self.cursor_pos)
				self.text=str(''.join(t))
			pl=((self.l)/len(self.text))
			self.cursor_pos=int((-self.x+pos1)//pl)
			if not self.cursor_pos>-1:
				self.cursor_pos=0
			elif self.cursor_pos>len(self.text):
				self.cursor_pos=len(self.text)
			t1=list(self.text)
			t1.insert(self.cursor_pos,self.cursor)
			self.text=str(''.join(t1))
			
	def change_line(self,pos):
	#	if ev.type==pygame.MOUSEBUTTONDOWN:
		x=0
		self.act=0
		if self.touch1(pos) and  self.x<self.x1 and not self.cursor_pos+1==len(self.text) :
			self.x+=10
			self.act=1
		elif self.x>self.x1:
			self.x=self.x1
		if self.touch2(pos) and self.x+self.l>self.x1+self.l1 :
			self.x-=10
			self.act=1
		elif self.x1<((self.l1+self.x1)-self.l) and self.l>self.l1 and self.cursor_pos==len(self.text):
			self.x=((self.l1+self.x1)-self.l)
	
	
			
	

wb=Input((255,255,255), 150,400,400,60,80)
p0=''
t=False
while True :
	display.fill((255,255,255)) 
	pos=pygame.mouse.get_pos()
	#fin=pygame.touch.get_finger()
	wb.change_line(pos)
	for ev in pygame.event.get():
		if ev.type==pygame.FINGERDOWN or ev.type==pygame.FINGERMOTION:
			if wb.touch(pos):
				pygame.key.start_text_input()
				p0=pos[0]
				wb.t=True
				wb.change_cursor_pos(pos,pos[0])
			else:
				p0=''
				wb.t=False
	#	if ev.type==pygame.MOUSEMOTION:	
		if wb.t==True:
			wb.edtext(ev)		
		#if ev.type==pygame.TEXTINPUT or ev.type==pygame.KEYUP:
		#	wb.t=True
		#else:
		#	wb.t=False
	label(display,f'{wb.text[-4:len(wb.text)]}',20,400,600)
#	label(display,f'{wb.cursor_pos}',40,600,600)
#	label(display,f'{ev}',10,0,700)
	wb.draw(display,p0)
	pygame.display.update()
