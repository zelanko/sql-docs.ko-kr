---
description: SQLConfigDataSource(Access 드라이버)
title: SQLConfigDataSource (Access 드라이버) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLConfigDataSource function [ODBC], Access Driver
- Access driver [ODBC], SQLConfigDataSource
ms.assetid: 1b152fb7-fa12-46b9-b168-006bb1355e77
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: deb777e0d1d4a4e3ea9a45968256ad23dbeb56ab
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88411989"
---
# <a name="sqlconfigdatasource-access-driver"></a>SQLConfigDataSource(Access 드라이버)
> [!NOTE]  
>  이 항목에서는 드라이버 관련 정보에 대 한 액세스를 제공 합니다. 이 함수에 대 한 일반 정보는 [ODBC API 참조](../../odbc/reference/syntax/odbc-api-reference.md)에서 적절 한 항목을 참조 하세요.  
  
 데이터 원본을 추가, 수정 또는 삭제 하는 데 사용 되는 **SQLConfigDataSource** 함수는 다음 키워드를 사용 합니다.  
  
|키워드|설명|  
|-------------|-----------------|  
|COLLATINGSEQUENCE|필드가 정렬 되는 순서입니다.<br /><br /> 이 옵션은 설정 대화 상자에서 **정렬 순서** 와 동일한 옵션을 설정 합니다.|  
|COMPACT_DB|데이터베이스 파일에 대 한 데이터 압축을 수행 합니다. 에는 COMPACT_DB =<path_name><\<optional ENCRYPT keyword> optionaL_sort_order>형식이 있습니다.<br /><br /> 동일한 문에서 DSN 키워드를 사용 하 여 COMPACT_DB 키워드를 사용 하는 경우이 드라이버는 DSN 키워드를 무시 합니다. 따라서 데이터베이스를 압축 하 고 DSN을 지정 하는 것은 2 단계 프로세스입니다.|  
|CREATE_DB|데이터베이스 파일을 만듭니다. 에는 다음 형식이 있습니다. CREATE_DB =<path_name>\<optional_sort-order><optional_ENCRYPT 키워드>. 여기서 경로 이름은 Microsoft Access 데이터베이스의 전체 경로입니다. 경로 이름에서 기존 데이터베이스를 지정 하면 오류가 반환 됩니다. Microsoft Access Setup 대화 상자에서 만들기 단추를 누르면 표시 되는 새 데이터베이스 대화 상자에 정렬 순서가 설정 됩니다. 정렬 순서가 지정 되지 않은 경우 일반이 사용 됩니다.<br /><br /> 동일한 문에서 DSN 키워드를 사용 하 여 CREATE_DB 키워드를 사용 하는 경우이 드라이버는 DSN 키워드를 무시 합니다. 따라서 데이터베이스를 만들고 DSN을 지정 하는 것은 2 단계 프로세스입니다. CREATE_DB 키워드를 사용할 때 만들 Microsoft Access 데이터베이스의 경로 이름에 하나 이상의 공백이 포함 된 경우 다음 예제와 같이 전체 경로 이름을 큰따옴표로 묶어야 합니다.<br /><br /> "C:\PROGRAM FILES\COMMON files\ MyAccess .mdb"<br /><br /> "C:\PROGRAM FILES\Access2.mdb"<br /><br /> CREATE_DB = C:\TEMP\test.mdb (인용 부호가 필요 하지 않음)|  
|CREATE_SYSDB|시스템 데이터베이스 파일을 만듭니다. 에는 CREATE_SYSDB = 형식이 있습니다. \<path-name> \<optional-sort-order> 여기서 경로 이름은 Microsoft Access 데이터베이스의 전체 경로입니다. 경로 이름에서 기존 데이터베이스를 지정 하면 오류가 반환 됩니다. 정렬 순서는 **ODBC Microsoft Access Setup** 대화 상자에서 **만들기** 단추를 클릭할 때 표시 되는 **새 데이터베이스** 대화 상자에 설정 됩니다. 정렬 순서가 지정 되지 않은 경우 일반이 사용 됩니다.|  
|CREATE_V2DB|Microsoft Access 2.0와 호환 되는 데이터베이스 파일을 만듭니다. 에는 CREATE_V2DB = 형식이 있습니다. \<path-name> \<optional-sort-order> 여기서 경로 이름은 Microsoft Access 데이터베이스의 전체 경로입니다. 경로 이름에서 기존 데이터베이스를 지정 하면 오류가 반환 됩니다. Microsoft Access Setup 대화 상자에서 만들기 단추를 누르면 표시 되는 새 데이터베이스 대화 상자에 정렬 순서가 설정 됩니다. 정렬 순서가 지정 되지 않은 경우 일반이 사용 됩니다.<br /><br /> 동일한 문에서 DSN 키워드를 사용 하 여 CREATE_V2DB 키워드를 사용 하는 경우이 드라이버는 DSN 키워드를 무시 합니다. 따라서 데이터베이스를 만들고 DSN을 지정 하는 것은 2 단계 프로세스입니다.<br /><br /> CREATE_V2DB 키워드를 사용할 때 만들 Microsoft Access 데이터베이스의 경로 이름에 하나 이상의 공백이 포함 된 경우 다음 예제와 같이 전체 경로 이름을 큰따옴표로 묶어야 합니다.<br /><br /> "C:\PROGRAM FILES\COMMON files\ MyAccess .mdb"<br /><br /> "C:\PROGRAM FILES\Access2.mdb"<br /><br /> CREATE_V2DB = C:\TEMP\test.mdb (인용 부호가 필요 하지 않음)|  
|DBQ|데이터베이스 파일의 이름입니다.<br /><br /> 이 옵션은 설치 대화 상자에서 **데이터베이스** 와 동일한 옵션을 설정 합니다.|  
|DEFAULTDIR|데이터베이스 파일에 대 한 경로 지정입니다.|  
|설명|데이터 원본의 데이터에 대 한 설명입니다.<br /><br /> 그러면 설정 대화 상자에서 **설명과** 동일한 옵션을 설정 합니다.|  
|DRIVER|드라이버 DLL에 대 한 경로 사양입니다.|  
|DRIVERID|드라이버의 정수 ID입니다.  25 (Microsoft Access)|  
|FIL|Microsoft Access에 대 한 파일 형식 MS 액세스|  
|IMPLICITCOMMITSYNC|Microsoft Access driver가 내부 또는 암시적 커밋을 비동기적으로 수행할지 여부를 결정 합니다. 처음에는이 값이 "예"로 설정 되어 있습니다. 즉, Microsoft Access 드라이버에서 내부/암시적 트랜잭션의 커밋이 완료 될 때까지 대기 합니다.<br /><br /> 이 옵션의 값은 결과를 신중 하 게 고려 하지 않으면 변경할 수 없습니다. 옵션에 대 한 자세한 내용은 *Microsoft Jet 데이터베이스 엔진 프로그래머 가이드*를 참조 하세요.<br /><br /> 이 옵션은 설치 대화 상자에서 **ImplicitCommitSync** 와 동일한 옵션을 설정 합니다.|  
|MAXBUFFERSIZE|Microsoft Access에서 디스크와 데이터를 전송 하는 데 사용 하는 내부 버퍼의 크기 (kb)입니다. 기본 버퍼 크기는 2048 KB (2048으로 표시)입니다. 256으로 나눌 수 있는 정수 값을 사용할 수 있습니다. 설정 대화 상자에서 **버퍼 크기** 와 동일한 옵션을 설정 합니다.|  
|MAXSCANROWS|기존 데이터에 기반 하 여 열의 데이터 형식을 설정할 때 검색할 행 수입니다.<br /><br /> 검색할 행에 대해 1에서 16 사이의 숫자를 입력할 수 있습니다. 값의 기본값은 8입니다. 0으로 설정 하면 모든 행이 검색 됩니다. 제한 밖의 숫자는 오류를 반환 합니다.<br /><br /> 이 옵션은 설치 대화 상자에서 **검색할 행** 과 동일한 옵션을 설정 합니다.|  
|PAGETIMEOUT|페이지가 제거 되기 전에 버퍼에 유지 되는 시간 (밀리초)을 지정 합니다. 기본값은 5-1/10 초 (0.5 초)입니다. 이 옵션은 ODBC 드라이버를 사용 하는 모든 데이터 원본에 적용 됩니다.<br /><br /> 설정 대화 상자에서 **페이지 시간 제한과** 같은 옵션을 설정 합니다.|  
|PWD|암호입니다.|  
|READONLY|파일을 읽기 전용으로 설정 하려면 TRUE로 설정 합니다. FALSE 이면 파일을 읽기 전용으로 설정 합니다.<br /><br /> 이 옵션은 설정 대화 상자에서 **읽기 전용** 과 동일한 옵션을 설정 합니다.|  
|REPAIR_DB|커밋 프로세스 중에 발생 한 오류에 의해 손상 된 데이터베이스를 복구 합니다.<br /><br /> 동일한 문에서 DSN 키워드를 사용 하 여 REPAIR_DB 키워드를 사용 하는 경우이 드라이버는 DSN 키워드를 무시 합니다. 따라서 데이터베이스를 복구 하 고 DSN을 지정 하는 과정은 두 단계로 진행 됩니다.|  
|SYSTEMDB|Microsoft Access driver의 경우 시스템 데이터베이스 파일에 대 한 경로 사양입니다.<br /><br /> 이 옵션은 설치 대화 상자에서 **시스템 데이터베이스** 와 동일한 옵션을 설정 합니다.|  
|임계값|엔진에서 사용할 백그라운드 스레드 수입니다. 이 값의 기본값은 3 이지만 변경할 수 있습니다.<br /><br /> 설정 대화 상자에서 **스레드와** 동일한 옵션을 설정 합니다.|  
|UID|Microsoft Access driver의 경우 로그인에 사용 되는 사용자 ID 이름입니다.|  
|USERCOMMITSYNC|Microsoft Access 드라이버에서 사용자 정의 트랜잭션을 비동기적으로 수행할지 여부를 결정 합니다. 처음에는이 값이 "예"로 설정 되어 있으므로 Microsoft Access 드라이버가 사용자 정의 트랜잭션의 커밋이 완료 될 때까지 대기 합니다.<br /><br /> 이 옵션의 값은 결과를 신중 하 게 고려 하지 않으면 변경할 수 없습니다. 옵션에 대 한 자세한 내용은 *Microsoft Jet 데이터베이스 엔진 프로그래머 가이드*를 참조 하세요.<br /><br /> 이 옵션은 설치 대화 상자에서 **Usercommitsync** 와 동일한 옵션을 설정 합니다.|
