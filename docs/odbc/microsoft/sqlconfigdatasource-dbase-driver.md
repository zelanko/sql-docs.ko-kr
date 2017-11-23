---
title: "SQLConfigDataSource (dBASE 드라이버) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: microsoft
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- DBase driver [ODBC], SQLConfigDataSource
- SQLConfigDataSource function [ODBC], dBASE Driver
ms.assetid: 19909902-054c-4e19-9c06-a212aace13fe
caps.latest.revision: "7"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 17b90ca3ab230aadaa764b58f3399172686502af
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/20/2017
---
# <a name="sqlconfigdatasource-dbase-driver"></a>SQLConfigDataSource (dBASE 드라이버)
> [!NOTE]  
>  이 항목에서는 dBASE 드라이버 관련 정보를 제공 합니다. 이 함수에 대 한 일반 정보에서 해당 항목을 참조 하십시오. [ODBC API 참조](../../odbc/reference/syntax/odbc-api-reference.md)합니다.  
  
 **SQLConfigDataSource** 함수를 추가 하는 데 사용 되는 수정 하거나 다음 키워드에 동적으로 사용 하 여 데이터 원본을 삭제 합니다.  
  
|키워드|Description|  
|-------------|-----------------|  
|COLLATINGSEQUENCE|필드 정렬 되는 시퀀스입니다.<br /><br /> 시퀀스 수: ASCII (기본값) 또는 국제 합니다.<br /><br /> 동일한 옵션을 설정 하는이 **데이터 정렬 시퀀스** 설정 대화 상자에서 합니다.|  
|DEFAULTDIR|디렉터리에 경로 지정 합니다.|  
|DELETED|DBASE 드라이버에 대 한 삭제 된 것으로 표시 된 행을 검색 또는에 배치 될 여부를 지정 합니다. 집합 1, 삭제 된 행에 표시 되지 않으면; 0, 삭제 된 행으로 설정 되 면 삭제 되지 않은 행과 동일 하 게 처리 합니다.<br /><br /> 동일한 옵션을 설정 하는이 **행 삭제 된 행 표시** 설정 대화 상자에서 합니다.|  
|DESCRIPTION|데이터 원본의 데이터에 대 한 설명<br /><br /> 동일한 옵션을 설정 하는이 **설명** 설정 대화 상자에서 합니다.|  
|DRIVER|드라이버 DLL 경로 지정 합니다.|  
|DRIVERID|드라이버는 정수 ID입니다.<br /><br /> 21 (dBASE III)<br /><br /> 277 (dBASE IV)<br /><br /> 533 (dBASE 5.0)|  
|FIL|파일 dBase III, IV, dBase 또는 dBase 5 입력 합니다.|  
|PAGETIMEOUT|페이지 (사용 되지 않음) 하는 경우 제거 하기 전에 버퍼에 남아 있는 초의 1/10 초에는 시간 기간을 지정 합니다. 기본값은 600 초 (60 초)의 1/10 초입니다. Note이 옵션은 ODBC 드라이버를 사용 하는 모든 데이터 원본에 적용 됩니다.<br /><br /> 동일한 옵션을 설정 하는이 **페이지 제한 시간** 설정 대화 상자에서 합니다.|  
|READONLY|파일을 만들기 위해 읽기 전용 이면 TRUE False 이면 읽기 전용 파일을 설정 합니다.<br /><br /> 동일한 옵션을 설정 하는이 **읽기 전용** 설정 대화 상자에서 합니다.|  
|STATISTICS|DBASE 드라이버에 대 한 테이블 크기 통계 근사화 됩니다 여부를 결정 합니다. Note이 옵션은 ODBC 드라이버를 사용 하는 모든 데이터 원본에 적용 됩니다.<br /><br /> 동일한 옵션을 설정 하는이 **대략적인 행 개수** 설정 대화 상자에서 합니다.|  
|스레드|사용 하도록 엔진에 대 한 백그라운드 스레드 수를 지정 합니다. 이 값은 3 이며 변경할 수 없습니다.<br /><br /> 동일한 옵션을 설정 하는이 **스레드** 설정 대화 상자에서 합니다.|
