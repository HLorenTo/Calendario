# Calendario
Construya el código fuente de un algoritmo que, dadas dos fechas entre agosto de 2020 y agosto de 2021, calcule el número de días hábiles entre dichas fechas teniendo en cuenta el calendario de Colombia?
import numpy as np
import datetime as dt
from datetime import date
import pandas as pd
from pandas.tseries.holiday import *
from pandas.tseries.offsets import CustomBusinessDay
print("Ingrese la fecha inicial dia, mes, año: ")
dia = (input()); mes = (input()); anio = (input())
fechauno = (dia +" "+mes+" "+anio+" ") ; print("Fecha uno: "+ fechauno)
print("Ingrese la fecha final dia, mes, año: ")
diaf = (input());mesf = (input()); aniof = (input())
fechados = (diaf +" "+mesf+" "+aniof+" ");  print("Fecha dos: "+ fechados)
if (anio > aniof):
    print("Año incorrecto: ")
dia = int(dia)
anio = int(anio)
mes = int(mes)
diaf = int(diaf)
aniof = int(aniof)
mesf = int(mesf)
fechafinal = date (aniof, mesf, diaf)
fechainicial = date (anio, mes, dia)
diastotal = fechafinal - fechainicial
print ("Total de días: ")
print (diastotal)
days = np.busday_count(fechainicial, fechafinal )
print ("Total de días laborales: ")
print (days)
class festivoscolombia(AbstractHolidayCalendar):
    rules = [
        Holiday('Año nuevo', month=1, day=1),
        Holiday('Día del trabajo', month=5, day=1),
        Holiday('Día de la independencia', month=7, day=20),
        Holiday('Batalla de Boyacá', month=8, day=7),
        Holiday('Inmaculada Concepción', month=12, day=8),
        Holiday('Navidad', month=12, day=25),
        Holiday('Jueves santo', month=1, day=1),
        Holiday('Viernes santo', month=1, day=1),
        Holiday('Ascención de Jesús', month=1, day=1),
        Holiday('Corpus Christi', month=1, day=1),
        Holiday('Sagrado Corazón de Jesús', month=1, day=1),
        Holiday('Epifanía del señor', month=1, day=6),
        Holiday('Día de San José', month=3, day=19),
        Holiday('San Pedro y San Pablo', month=6, day=29),
        Holiday('Asunción de la Virgen', month=8, day=15),
        Holiday('Día de la raza', month=10, day=12),
        Holiday('Todos los santos', month=11, day=1),
        Holiday('Independencia de Cartagena', month=11, day=11)
Colombian_BD = CustomBusinessDay(calendar=festivoscolombia());
s = pd.date_range(fechainicial, fechafinal, freq=Colombian_BD)
df = pd.DataFrame(s, columns=['Date'])
print("Días laborales sin festivos")
print(df)
