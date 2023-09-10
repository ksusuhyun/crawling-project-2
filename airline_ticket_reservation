# 학생1('네이버'라는 사이트에서 출발지와 도착지를 입력하면 예매 정보를 출력하는 크롤러를 크롤링)
from selenium import webdriver
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.support import expected_conditions as EC
from selenium.webdriver.common.by import By
from datetime import date
import openpyxl

def wait_until(xpath_str):
    WebDriverWait(browser,30).until(EC.presence_of_element_located
    ((By.XPATH,xpath_str)))

browser=webdriver.Chrome()
url='https://flight.naver.com/'
browser.get(url)

begin_date=browser.find_element(By.XPATH, '//button[text()="가는 날"]')
begin_date.click()


now=date.today().month
count=9-now

wait_until('//b[text()="8"]')
day8=browser.find_elements(By.XPATH, '//b[text()="8"]')
day8[count].click()


wait_until('//b[text()="16"]')
day16=browser.find_elements(By.XPATH, '//b[text()="16"]')
day16[count].click()


wait_until('//b[text()="도착"]')
arrival=browser.find_element(By.XPATH, '//b[text()="도착"]')
arrival.click()

wait_until('//button[text()="유럽"]')
europe=browser.find_element(By.XPATH, '//button[text()="유럽"]')
europe.click()

wait_until('//i[text()="샤를드골국제공항"]')
CDG=browser.find_element(By.XPATH, '//i[text()="샤를드골국제공항"]')
CDG.click()



wait_until('//button[text()="직항만"]')
direct=browser.find_element(By.XPATH, '//button[text()="직항만"]')
direct.click()



wait_until('//span[text()="항공권 검색"]')
search=browser.find_element(By.XPATH, '//span[text()="항공권 검색"]')
search.click()

wait_until('//div[@class="concurrent_ConcurrentItemContainer__2lQVG result"]')
element=browser.find_elements(By.XPATH, ('//div[@class="concurrent_ConcurrentItemContainer__2lQVG result"]'))


wb=openpyxl.Workbook()
sheet=wb.active
sheet.append(["항공사","출발시간","도착시간","직항여부","비행시간","항공사","출발시간","도착시간","직항여부","비행시간"])


r=1
c=0
for e in element:
    e1=e.text.splitlines()
    r+=1
    c=0
    for t in e1:
        c+=1
        sheet.cell(row=r,column=c).value=t
        print(t)

wb.save("data.csv")
input('종료하려면 아무키나 누르세요')
browser.quit()

#학생 2('네이버'라는 사이트에서 출발지와 도착지를 입력하면 가격을 출력하는 크롤러를 크롤링)
from selenium import webdriver
from selenium.webdriver.common.keys import Keys
import time

driver = webdriver.Chrome()
driver.get("https://flight.naver.com/")
time.sleep(1)

def airway(parts):
    for part in parts:
        index = parts.index(part)
        driver.find_element_by_xpath(f'//*[@id="__next"]/div/div[1]/div[4]/div/div/div[2]/div[1]/button[{int(index)+1}]').click()
        driver.find_element_by_xpath('//*[@id="__next"]/div/div[1]/div[9]/div[1]/div/input').send_keys(part)
        time.sleep(0.1)
        driver.find_element_by_xpath('//*[@id="__next"]/div/div[1]/div[9]/div[2]/section/div').click()
        time.sleep(0.5)
def select_dates(month, week, day):
    print(f"week 번호 : {week}   요일 번호 : {day}")
    driver.find_element_by_xpath(f'//*[@id="__next"]/div/div[1]/div[9]/div[2]/div[1]/div[2]/div/div[{month}]/table/tbody/tr[{week}]/td[{day}]/button/b').click()
    time.sleep(0.1)

ports = {'김포':'GMP','인천':'ICN','제주':'CJU','김해':'PUS','대구':'TAE'}
points = [ports['김포'],ports['제주']]
print(points)
airway(points)

driver.find_element_by_xpath('//*[@id="__next"]/div/div[1]/div[4]/div/div/div[2]/div[2]/button[1]').click()
time.sleep(1)

month = 2
week = 3
day_go = '토요일'
day_n_nights = 4

days = ['일요일', '월요일', '화요일', '수요일', '목요일', '금요일', '토요일']
day = days.index(day_go)+1      
select_dates(month, week, day)  
day = day+day_n_nights-1       

if day > 7:
    week+=day//7
    day = day%7
try:
    select_dates(month, week, day)
except:
    if week >= 4:
        month += 1
        week = 1
        select_dates(month, week, day)


driver.find_element_by_xpath('//*[@id="__next"]/div/div[1]/div[4]/div/div/button').click()

delay = 10
for i in range(delay):
    time.sleep(1)
    print(f'{delay-i}초 후 실행됩니다.')

from bs4 import BeautifulSoup as bs


for i in range(10):
    driver.execute_script("window.scrollTo(0, document.body.scrollHeight)")
    time.sleep(0.2)

page_url = driver.page_source
soup = bs(page_url, "html.parser")
flights = soup.find_all(class_='result')

for flight in flights:
    print(flight.text)

print(f'총 {len(flights)}개의 항공권 정보를 불러왔습니다.')
