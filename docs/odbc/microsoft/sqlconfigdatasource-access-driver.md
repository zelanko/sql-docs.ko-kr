---
title: SQLConfigDataSource (Access 드라이버) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- SQLConfigDataSource function [ODBC], Access Driver
- Access driver [ODBC], SQLConfigDataSource
ms.assetid: 1b152fb7-fa12-46b9-b168-006bb1355e77
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f6e6927524bd590d4dde2b8db215f15e2a937e2b
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="sqlconfigdatasource-access-driver"></a>SQLConfigDataSource (Access 드라이버)
> [!NOTE]  
>  이 항목에서는 액세스 드라이버 관련 정보를 제공 합니다. 이 함수에 대 한 일반 정보에서 해당 항목을 참조 하십시오. [ODBC API 참조](../../odbc/reference/syntax/odbc-api-reference.md)합니다.  
  
 **SQLConfigDataSource** 함수를 추가 하는 데 사용 되는 수정 하거나 다음 키워드에 동적으로 사용 하 여 데이터 원본을 삭제 합니다.  
  
|키워드|Description|  
|-------------|-----------------|  
|COLLATINGSEQUENCE|필드 정렬 되는 시퀀스입니다.<br /><br /> 동일한 옵션을 설정 하는이 **데이터 정렬 시퀀스** 설정 대화 상자에서 합니다.|  
|COMPACT_DB|데이터베이스 파일에 데이터 압축을 수행합니다. 형식은 다음과 같습니다: COMPACT_DB < path_name >< optionaL_sort_order > =\<선택적 암호화 키워드 > 합니다.<br /><br /> DSN 키워드와 함께 동일한 문에서 COMPACT_DB 키워드를 사용 하는 경우이 드라이버는 DSN 키워드를 무시 합니다. 따라서 데이터베이스를 압축 하 고 DSN을 지정 하는 단계로 수행 됩니다.|  
|CREATE_DB|데이터베이스 파일을 만듭니다. 형식은 다음과 같습니다: CREATE_DB < path_name > =\<optional_sort 순서 >< optional_ENCRYPT 키워드 > 경로 이름은 Microsoft Access 데이터베이스에 전체 경로입니다. 경로 이름을 기존 데이터베이스를 지정 하는 경우 오류가 반환 됩니다. 정렬 순서가 됩니다 세트로 Microsoft Access 설정 대화 상자에서 만들기 단추를 누를 때 표시 되는 새 데이터베이스 대화 상자. 정렬 순서가 없는 지정 하는 경우 일반 사용 됩니다.<br /><br /> DSN 키워드와 함께 동일한 문에서 CREATE_DB 키워드를 사용 하는 경우이 드라이버는 DSN 키워드를 무시 합니다. 따라서 데이터베이스 만들기 및 DSN이 지정 하는 단계로 수행 됩니다. 를 만들 Microsoft Access 데이터베이스의 경로 이름에 공백이 있으면 하나 이상의 CREATE_DB 키워드를 사용할 때 다음 전체 경로 이름은로 묶어야 합니다 큰따옴표를 다음 예제에 나와 있는 것 처럼:<br /><br /> "C:\PROGRAM FILES\COMMON FILES\ MyAccess.mdb"<br /><br /> "C:\PROGRAM FILES\Access2.mdb"<br /><br /> CREATE_DB=C:\TEMP\test.mdb (인용 부호 제외 필요)|  
|CREATE_SYSDB|시스템 데이터베이스 파일을 만듭니다. 형식은 다음과 같습니다: CREATE_SYSDB =\<경로 이름 >\<정렬 순서 옵션 >, 여기서 경로 name은 Microsoft Access 데이터베이스에 전체 경로입니다. 경로 이름을 기존 데이터베이스를 지정 하는 경우 오류가 반환 됩니다. 정렬 순서에 포함 됩니다 세트로는 **새 데이터베이스** 때 표시 된 대화 상자는 **만들기** 에서 단추를 클릭는 **열려는 데이터베이스 액세스** 대화 상자. 정렬 순서가 없는 지정 하는 경우 일반 사용 됩니다.|  
|CREATE_V2DB|Microsoft Access 2.0와 호환 되는 데이터베이스 파일을 만듭니다. 형식은 다음과 같습니다: CREATE_V2DB =\<경로 이름 >\<정렬 순서 옵션 >, 여기서 경로 name은 Microsoft Access 데이터베이스에 전체 경로입니다. 경로 이름을 기존 데이터베이스를 지정 하는 경우 오류가 반환 됩니다. 정렬 순서가 됩니다 세트로 Microsoft Access 설정 대화 상자에서 만들기 단추를 누를 때 표시 되는 새 데이터베이스 대화 상자. 정렬 순서가 없는 지정 하는 경우 일반 사용 됩니다.<br /><br /> DSN 키워드와 함께 동일한 문에서 CREATE_V2DB 키워드를 사용 하는 경우이 드라이버는 DSN 키워드를 무시 합니다. 따라서 데이터베이스 만들기 및 DSN이 지정 하는 단계로 수행 됩니다.<br /><br /> 를 만들 Microsoft Access 데이터베이스의 경로 이름에 공백이 있으면 하나 이상의 CREATE_V2DB 키워드를 사용할 때 다음 전체 경로 이름은로 묶어야 합니다 큰따옴표를 다음 예제에 나와 있는 것 처럼:<br /><br /> "C:\PROGRAM FILES\COMMON FILES\ MyAccess.mdb"<br /><br /> "C:\PROGRAM FILES\Access2.mdb"<br /><br /> CREATE_V2DB=C:\TEMP\test.mdb (인용 부호 제외 필요)|  
|DBQ|데이터베이스 파일의 이름입니다.<br /><br /> 동일한 옵션을 설정 하는이 **데이터베이스** 설정 대화 상자에서 합니다.|  
|DEFAULTDIR|데이터베이스 파일에 경로 지정 합니다.|  
|DESCRIPTION|데이터 원본의 데이터에 대 한 설명<br /><br /> 동일한 옵션을 설정 하는이 **설명** 설정 대화 상자에서 합니다.|  
|DRIVER|드라이버 DLL 경로 지정 합니다.|  
|DRIVERID|드라이버는 정수 ID입니다.  25 (Microsoft Access)|  
|FIL|파일 유형 Microsoft Access에 대 한 MS 액세스|  
|IMPLICITCOMMITSYNC|Microsoft Access 드라이버 내부 또는 암시적 커밋이 비동기적으로 수행 여부를 결정 합니다. 이 값은 처음 의미 Microsoft Access 드라이버 완료 하는 데 내부/암시적 트랜잭션 커밋을 대기 하는 "예"로 설정 됩니다.<br /><br /> 그 결과 신중 하 게 고려 하지 않고이 옵션의 값을 변경할 수 없습니다. 옵션에 대 한 자세한 내용은 참조는 *Microsoft Jet 데이터베이스 엔진 Programmer's Guide*합니다.<br /><br /> 동일한 옵션을 설정 하는이 **ImplicitCommitSync** 설정 대화 상자에서 합니다.|  
|MAXBUFFERSIZE|내부 버퍼의 (킬로바이트), 디스크에서 데이터를 전송 하려면 Microsoft Access에서 사용 되는 크기입니다. 기본 버퍼 크기는 2048 KB (2048으로 표시 됨). 256로 나눌 정수 값을 사용할 수 있습니다. 동일한 옵션을 설정 하는이 **버퍼 크기** 설정 대화 상자에서 합니다.|  
|MAXSCANROWS|기존 데이터에 따라 열의 데이터 형식을 설정할 때 검사할 행의 수입니다.<br /><br /> 검색할 행에 대 한 16 개가 하 1에서 숫자를 입력할 수 있습니다. 기본값은 8; 0으로 설정 하는 경우 모든 행이 검색 됩니다. (제한 벗어나는 숫자 오류가 반환 됩니다.)<br /><br /> 동일한 옵션을 설정 하는이 **검색할 행** 설정 대화 상자에서 합니다.|  
|PAGETIMEOUT|시간, 페이지 (사용 되지 않음) 하는 경우 제거 하기 전에 버퍼에 남아 있는 밀리초 단위로 지정 합니다. 기본값은 5-1/10 초 (0.5 초)입니다. Note이 옵션은 ODBC 드라이버를 사용 하는 모든 데이터 원본에 적용 됩니다.<br /><br /> 동일한 옵션을 설정 하는이 **페이지 제한 시간** 설정 대화 상자에서 합니다.|  
|PWD|암호입니다.|  
|READONLY|파일을 만들기 위해 읽기 전용 이면 TRUE False 이면 읽기 전용 파일을 설정 합니다.<br /><br /> 동일한 옵션을 설정 하는이 **읽기 전용** 설정 대화 상자에서 합니다.|  
|REPAIR_DB|커밋 중에 발생 하는 오류로 인해 손상 된 데이터베이스를 복구 합니다.<br /><br /> DSN 키워드와 함께 동일한 문에서 REPAIR_DB 키워드를 사용 하는 경우이 드라이버는 DSN 키워드를 무시 합니다. 따라서는 데이터베이스를 복구 하 고 DSN을 지정 하는 단계로 수행 됩니다.|  
|SYSTEMDB|Microsoft Access 드라이버를 시스템 데이터베이스 파일에 경로 지정 합니다.<br /><br /> 동일한 옵션을 설정 하는이 **시스템 데이터베이스** 설정 대화 상자에서 합니다.|  
|스레드|사용 하도록 엔진에 대 한 백그라운드 스레드 수를 지정 합니다. 이 값을 3으로 기본값만 변경할 수 있습니다.<br /><br /> 동일한 옵션을 설정 하는이 **스레드** 설정 대화 상자에서 합니다.|  
|UID|Microsoft Access 드라이버에 대 한 로그인에 사용자 ID 이름을 사용 합니다.|  
|USERCOMMITSYNC|Microsoft Access 드라이버 사용자 정의 트랜잭션을 비동기적으로 수행 여부를 결정 합니다. 이 값은 처음 의미 Microsoft Access 드라이버 완료 하는 데 사용자 정의 트랜잭션 커밋을 대기 하는 "예"로 설정 됩니다.<br /><br /> 그 결과 신중 하 게 고려 하지 않고이 옵션의 값을 변경할 수 없습니다. 옵션에 대 한 자세한 내용은 참조는 *Microsoft Jet 데이터베이스 엔진 Programmer's Guide*합니다.<br /><br /> 동일한 옵션을 설정 하는이 **UserCommitSync** 설정 대화 상자에서 합니다.|
