# rail-location-ELK

- ๐ฑ APP

    - Language & Environment: docker (20.10.14), docker-compose (2.3.4)

    - Library : elasticsearch, logstash, kibana 8.1.2

    - Developer : ํ์น์ฐ

# ๊ฐ์
๊ณต๊ณต ๋ฐ์ดํฐ์ ELK Stack์ ํ์ฉํ ์งํ์ฒ  ์ญ ์์น ์๊ฐํ 

![์ด๋ฏธ์ง](https://github.com/kaintels/rail-location-ELK/blob/main/img/main.png)

# ์ฌ์ฉ๋ฐฉ๋ฒ

๋์ปค ์ปดํฌ์ฆ ์ฌ์ฉ 
```
docker-compose build && docker-compose up -d
```

๋ฐ์ดํฐ ๋ค์ด๋ก๋ (์ดํ MySQL(MariaDB)์ ์ ์ฅ)

[์ฌ์ฉํ ๊ณต๊ณต๋ฐ์ดํฐ](https://www.data.go.kr/tcs/dss/selectDataSetList.do?dType=FILE&keyword=%EC%88%98%EB%8F%84%EA%B6%8C+%EC%97%AD%EC%9C%84%EC%B9%98&detailKeyword=&publicDataPk=&recmSe=N&detailText=&relatedKeyword=&commaNotInData=&commaAndData=&commaOrData=&must_not=&tabId=&dataSetCoreTf=&coreDataNm=&sort=_score&relRadio=&orgFullName=&orgFilter=&org=&orgSearch=&currentPage=1&perPage=10&brm=&instt=&svcType=&kwrdArray=&extsn=&coreDataNmArray=&pblonsipScopeCode=)


๋ก๊ทธ์คํ์ log ์กฐํ (์ปจํ์ด๋ ์ด๋ฆ์ด logstash์ผ ๊ฒฝ์ฐ)
```
docker-compose logs logstash
```

kibana - > dev tools์์ ์ธ๋ฑ์ค ํํ๋ฆฟ ์์ฑ
```
PUT _index_template/station_info
{
	"index_patterns": ["station_info*"],
	"template": {
	  "settings": {
	    "number_of_shards": 1
	  },
	  "mappings": {
	    "properties":{
	      "locations":{
	        "type": "geo_point"
	      }
	    }
	  }
	}
}
```

๋์ปค ์ปดํฌ์ฆ ์ฌ์์
```
docker-compose restart
```
