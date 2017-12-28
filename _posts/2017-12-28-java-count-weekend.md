---
layout: post
title: "Calendar class를 이용한 주말 일 수 구하기"
tags: "java","Calendar"
comments: true
categories : Calendar
---
# Calendar class를 이용한 주말 일 수 구하기
회사 업무 중 휴가 일수를 체크하는 로직에서 주말은 빼줘야 했다. 
이전에 근태 관련해서 개발을 할 때 Calendar 클래스에서 요일을 가져오는걸 확인


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