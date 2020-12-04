# python-爬去拉钩网
from selenium.webdriver  import Chrome      #导入浏览器的包--自动化进程
from selenium.webdriver.common.keys import Keys
import time

#创建浏览器
web =Chrome()
#打开浏览器，请求到拉勾网
web.get('https://www.lagou.com')
web.find_element_by_xpath('//*[@id="cboxClose"]').click()   

#来个时间反应延迟
time.sleep(1)

#找到搜索文本框，自动输入python ，之后输入回车
web.find_element_by_xpath('//*[@id="search_input"]').send_keys('python',Keys.ENTER)
n=1

web.find_element_by_xpath("/html/body/div[9]/div/div[2]") .click()
list=web.find_elements_by_class_name('position_link')     

for a in list:          #再从列表中找出所有  a  标签
    a.find_element_by_tag_name('h3').click()    #找到所有的超链接  h3  ,并自动点击
    #窗口转换（跳转 ）
    web.switch_to .window(web.window_handles[-1])       #跳转到倒数第一个窗口
    
    #拿招聘信息
    text=web.find_element_by_xpath('//*[@id="job_detail"]/dd[2]/div').text   #拿文本

    #把招聘信息保存文件中
    f=open('abc/需求_%s.txt'%n,mode='w')
    f.write(text)
    f.close()           #关闭文件


    #关闭窗口
    web.close()
    #调整窗口到最开始的页面
    web.switch_to.window(web.window_handles[0])
    time.sleep(1)

    n+=1
