---
layout: post
title: "Java Calendar class를 이용한 주말 일 수 구하기"
tags: "java"
comments: true
categories : Jekyll  
---

### 문제 : 
휴가일수 데이터를 다른 서비스와 연동하려고 한다. 휴가일 수 이다 보니 주말같은 공휴일이 중간에 끼는 경우 체크해서 빼줘야 한다. 

### 해결책 : 
이전에 개인 근태 관련된 코드를 작성하면서 `Calendar` 클래스를 사용하면 날짜별로 요일을 구해올 수 있었다. 

시작일과 종료일을 각각의 `Calendar Instance`에 담고 해당 일수를 for문 돌려서 주말인 경우만 count를 늘려 준다. 

``` java 
import java.text.SimpleDateFormat;
import java.util.Calendar;
import java.util.Date;

public int findWeekendCnt(String startdate, String enddate) throws Exception {
    int weekendCnt = 0;
    Calendar.getInstance().setTime( new SimpleDateFormat("yyyyMMdd").parse(startdate) );
    Date endDate = new SimpleDateFormat("yyyyMMdd").parse(enddate);
    Date startDate = new SimpleDateFormat("yyyyMMdd").parse(startdate);
    Calendar startCal = Calendar.getInstance();
    Calendar endCal = Calendar.getInstance();
    Calendar compareCal = Calendar.getInstance();
    startCal.setTime(startDate);
    endCal.setTime(endDate);
    endCal.add(Calendar.DATE, 1);
    for( Date date = startCal.getTime(); startCal.before(endCal); 
            startCal.add(Calendar.DATE, 1), date = startCal.getTime()) {
        compareCal.setTime(date);
        int dayNum = compareCal.get(Calendar.DAY_OF_WEEK);
        switch(dayNum) {
            case 1: weekendCnt++; break;
            case 7: weekendCnt++; break;
        }
    }
    return weekendCnt;
}
```
### 참고 :


