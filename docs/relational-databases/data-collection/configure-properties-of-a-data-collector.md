---
title: "데이터 수집기의 속성 구성 | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.swb.dc.datacollectionprop.general.f1"
  - "sql13.swb.dc.datacollectionprop.advanced.f1"
ms.assetid: cf98f57d-5a6d-4bc3-bf10-783e460fc63d
caps.latest.revision: 5
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 5
---
# 데이터 수집기의 속성 구성
  이 항목에서는 데이터 수집기의 속성을 구성하는 방법에 대해 설명합니다.  
  
## 데이터 컬렉션 속성(일반 탭)  
 이 페이지를 사용하여 관리 데이터 웨어하우스에 대한 설정을 구성하고 수집한 데이터를 데이터 웨어하우스에 업로드하기 전에 저장하는 위치를 지정할 수 있습니다.  
  
 **데이터 컬렉션 활성화**  
 데이터 컬렉션을 사용하려면 선택합니다. 이렇게 하면 sp_syscollector_enable_collector 저장 프로시저를 실행하는 것과 같은 결과가 나타납니다. 이 확인란의 선택을 취소하면 데이터 컬렉션이 사용되지 않고 sp_syscollector_disable_collector 저장 프로시저를 실행하는 것과 같은 결과가 나타납니다.  
  
 **Server**  
 관리 데이터 웨어하우스를 호스팅할 서버의 이름을 표시합니다.  
  
 **데이터베이스 이름**  
 관리 데이터 웨어하우스에 사용되는 관계형 데이터베이스의 이름을 표시합니다.  
  
 **연결 테스트**  
 데이터 컬렉션이 구성될 때 제공된 정보를 사용하여 지정된 **서버**에 대한 연결을 테스트합니다.  
  
 **캐시 디렉터리**  
 수집된 데이터를 관리 데이터 웨어하우스에 업로드하기 전에 데이터를 수집하는 시스템에 저장할 디렉터리를 지정합니다. **캐시 디렉터리** 를 지정하지 않으면 데이터 수집기가 %TEMP% 및 %TMP% 환경 변수를 찾고 이러한 위치 중 하나를 임시 저장소의 기본 위치로 사용하려고 합니다. 이러한 환경 변수가 구성되어 있지 않으면 오류가 발생하고 캐시 디렉터리를 만들라는 메시지가 나타납니다.  
  
## 데이터 컬렉션 속성(고급 탭)  
 이 페이지를 사용하여 관리 데이터 웨어하우스에 연결하는 데 사용되는 다시 시도 설정을 구성할 수 있습니다.  
  
 **업로드 실패 시의 다시 시도 횟수**  
 관리 데이터 웨어하우스에 대한 업로드가 실패할 경우 다시 시도할 횟수를 지정합니다. 기본값은 1입니다.  
  
## 참고 항목  
 [데이터 컬렉션 관리](../../relational-databases/data-collection/manage-data-collection.md)   
 [관리 데이터 웨어하우스 구성&#40;SQL Server Management Studio&#41;](../../relational-databases/data-collection/configure-the-management-data-warehouse-sql-server-management-studio.md)  
  
  