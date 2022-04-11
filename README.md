# rail-location-ELK

- 📱 APP

    - Language & Environment: docker (20.10.14), docker-compose (2.3.4)

    - Library : elasticsearch, logstash, kibana 8.1.2

    - Developer : 한승우

# 개요
공공 데이터와 ELK Stack을 활용한 지하철 역 위치 시각화 

![이미지](https://github.com/kaintels/rail-location-ELK/blob/main/img/main.png)

# 사용방법

도커 컴포즈 사용 
```
docker-compose build && docker-compose up -d
```

데이터 다운로드 (이후 MySQL(MariaDB)에 저장)

[사용한 공공데이터](https://www.data.go.kr/tcs/dss/selectDataSetList.do?dType=FILE&keyword=%EC%88%98%EB%8F%84%EA%B6%8C+%EC%97%AD%EC%9C%84%EC%B9%98&detailKeyword=&publicDataPk=&recmSe=N&detailText=&relatedKeyword=&commaNotInData=&commaAndData=&commaOrData=&must_not=&tabId=&dataSetCoreTf=&coreDataNm=&sort=_score&relRadio=&orgFullName=&orgFilter=&org=&orgSearch=&currentPage=1&perPage=10&brm=&instt=&svcType=&kwrdArray=&extsn=&coreDataNmArray=&pblonsipScopeCode=)


로그스태시 log 조회
```
docker-compose logs d
```

kibana - > dev tools에서 인덱스 템플릿 생성
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

도커 컴포즈 재시작
```
docker-compose restart
```
