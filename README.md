# Web_scraping_formate


# Web_scraping_formate


        import pandas as pd
        from bs4 import BeautifulSoup
        import requests
        import numpy as np 


        final = pd.DataFrame()

        for j in range(1,10):
            website = requests.get("https://www.yellowpages.com/glendale-ca/physicians-surgeons?page={}".format(j)).text
            soup = BeautifulSoup(website, 'lxml')
            doctor = soup.find_all('div', class_='v-card')


            name=[]
            street=[]
            location=[]
            phone=[]
            how_old=[]
            service=[]
            rating=[]
[Doctor.csv](https://github.com/dsanisur/Web_scraping_formate/files/10723529/Doctor.csv)



            for i in doctor:
                try:
                    name.append(i.find('h2').text)
                except:
                    name.append(np.nan)
                try:
                    street.append(i.find('div',class_='street-address').text)
                except:
                    street.append(np.nan)
                try:
                    location.append(i.find('div',class_='locality').text)
                except:
                    location.append(np.nan)
                try:
                    phone.append(i.find('div',class_='phone').text)
                except:
                    phone.append(np.nan)
                try:
                    how_old.append(i.find('div','number').text)
                except:
                    how_old.append(np.nan)
                try:
                    service.append(i.find('div',class_='categories').text)
                except:
                    service.append(np.nan)
                try:
                    rating.append(i.find("span",class_="count").text)
                except:
                    rating.append(np.nan)

            d = pd.DataFrame({"Name":name,
                "street":street,
                'Location':location,
                "phone":phone,
                "service":service,
                "rating":rating})

            final = final.append(d,ignore_index=True)
        final.to_csv("Doctor.csv")
