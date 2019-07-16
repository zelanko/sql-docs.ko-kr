---
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 85b515ed4c30d68e62a49e1044c4ddf6f5cc5ab1
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67985240"
---
# <a name="sqlconfigdatasource-access-driver"></a>SQLConfigDataSource(Access 드라이버)
> [!NOTE]  
>  이 항목에서는 액세스 드라이버 관련 정보를 제공 합니다. 이 함수에 대 한 일반 정보에서 해당 항목을 참조 하세요 [ODBC API 참조](../../odbc/reference/syntax/odbc-api-reference.md)합니다.  
  
 합니다 **SQLConfigDataSource** 함수를 추가 하는 데 사용 되는 수정 또는 데이터 원본 삭제 동적으로 다음과 같은 키워드를 사용 합니다.  
  
|키워드|설명|  
|-------------|-----------------|  
|COLLATINGSEQUENCE|필드 정렬 되는 시퀀스입니다.<br /><br /> 동일한 옵션을 설정 **데이터 정렬 시퀀스** 설정 대화 상자에서.|  
|COMPACT_DB|데이터베이스 파일에서 데이터 압축을 수행합니다. 다음 형식은 같습니다. COMPACT_DB < path_name >< optionaL_sort_order > =\<선택적 암호화 키워드 >.<br /><br /> DSN 키워드를 사용 하 여 동일한 문에서 COMPACT_DB 키워드를 사용 하는 경우이 드라이버는 DSN 키워드를 무시 합니다. 따라서 데이터베이스를 압축 하 고 DSN을 지정 하는 두 단계로 이루어집니다.|  
|CREATE_DB|데이터베이스 파일을 만듭니다. 다음 형식은 같습니다. CREATE_DB < path_name > =\<optional_sort 순서 >< optional_ENCRYPT 키워드 > 경로 이름은 Microsoft Access 데이터베이스에 전체 경로입니다. 경로 이름을 기존 데이터베이스를 지정 하는 경우 오류가 반환 됩니다. 정렬 순서가 됩니다 세트로 Microsoft 액세스 설정 대화 상자에서 만들기 단추를 누를 때 표시 되는 새 데이터베이스 대화 상자에서. 정렬 순서가 지정 되지 않은, 경우에 일반 사용 됩니다.<br /><br /> DSN 키워드를 사용 하 여 동일한 문에서 CREATE_DB 키워드를 사용 하는 경우이 드라이버는 DSN 키워드를 무시 합니다. 따라서 데이터베이스를 만들고 DSN을 지정 하는 두 단계로 이루어집니다. 만들려는 Microsoft Access 데이터베이스의 경로 이름에 공백이 있으면 하나 이상의 CREATE_DB 키워드를 사용 하는 경우 다음 전체 경로 이름으로 묶어야 합니다 큰따옴표 다음 예와에서 같이:<br /><br /> "C:\PROGRAM FILES\COMMON FILES\ MyAccess.mdb"<br /><br /> "C:\PROGRAM FILES\Access2.mdb"<br /><br /> CREATE_DB=C:\TEMP\test.mdb (따옴표 필요)|  
|CREATE_SYSDB|시스템 데이터베이스 파일을 만듭니다. 다음 형식은 같습니다. CREATE_SYSDB =\<경로 이름 >\<정렬 순서 옵션 > 경로 이름은 Microsoft Access 데이터베이스에 전체 경로 합니다. 경로 이름을 기존 데이터베이스를 지정 하는 경우 오류가 반환 됩니다. 정렬 됩니다 집합으로 구성 합니다 **새 데이터베이스** 대화 상자를 표시 하는 경우를 **만들기** 에서 단추를 클릭 합니다 **ODBC Microsoft 액세스 설정** 대화 상자. 정렬 순서가 지정 되지 않은, 경우에 일반 사용 됩니다.|  
|CREATE_V2DB|Microsoft Access 2.0 호환 되는 데이터베이스 파일을 만듭니다. 다음 형식은 같습니다. CREATE_V2DB =\<경로 이름 >\<정렬 순서 옵션 > 경로 이름은 Microsoft Access 데이터베이스에 전체 경로 합니다. 경로 이름을 기존 데이터베이스를 지정 하는 경우 오류가 반환 됩니다. 정렬 순서가 됩니다 세트로 Microsoft 액세스 설정 대화 상자에서 만들기 단추를 누를 때 표시 되는 새 데이터베이스 대화 상자에서. 정렬 순서가 지정 되지 않은, 경우에 일반 사용 됩니다.<br /><br /> DSN 키워드를 사용 하 여 동일한 문에서 CREATE_V2DB 키워드를 사용 하는 경우이 드라이버는 DSN 키워드를 무시 합니다. 따라서 데이터베이스를 만들고 DSN을 지정 하는 두 단계로 이루어집니다.<br /><br /> 만들려는 Microsoft Access 데이터베이스의 경로 이름에 공백이 있으면 하나 이상의 CREATE_V2DB 키워드를 사용 하는 경우 다음 전체 경로 이름으로 묶어야 합니다 큰따옴표 다음 예와에서 같이:<br /><br /> "C:\PROGRAM FILES\COMMON FILES\ MyAccess.mdb"<br /><br /> "C:\PROGRAM FILES\Access2.mdb"<br /><br /> CREATE_V2DB=C:\TEMP\test.mdb (따옴표 필요)|  
|DBQ|데이터베이스 파일의 이름입니다.<br /><br /> 동일한 옵션을 설정 **데이터베이스** 설정 대화 상자에서.|  
|DEFAULTDIR|데이터베이스 파일에 경로 지정 합니다.|  
|DESCRIPTION|데이터 원본에 있는 데이터의 설명입니다.<br /><br /> 동일한 옵션을 설정 **설명을** 설정 대화 상자에서.|  
|DRIVER|드라이버 DLL 경로 지정 합니다.|  
|DRIVERID|드라이버에 대 한 정수 ID입니다.  25 (Microsoft Access)|  
|FIL|파일 형식을 Microsoft Access에 대 한 MS 액세스|  
|IMPLICITCOMMITSYNC|Microsoft Access 드라이버를 내부 또는 암시적 커밋을 비동기적으로 수행 하는지 여부를 결정 합니다. 이 값은 처음에 Microsoft Access 드라이버를 완료할 수 있도록 내부/암시적 트랜잭션 커밋을 대기 함을 의미는 "예"로 설정 됩니다.<br /><br /> 그 결과에 신중 하 게 고려 하지 않고이 옵션의 값을 변경할 수 없습니다. 옵션에 대 한 자세한 내용은 참조는 *Microsoft Jet 데이터베이스 엔진 Programmer's Guide*합니다.<br /><br /> 동일한 옵션을 설정 **ImplicitCommitSync** 설정 대화 상자에서.|  
|MAXBUFFERSIZE|내부 버퍼의 (킬로바이트)에서 디스크에서 데이터를 전송 하려면 Microsoft Access에서 사용 되는 크기입니다. 기본 버퍼 크기는 2048KB (2048로 표시 됨). 256 나눌 정수 값을 사용할 수 있습니다. 동일한 옵션을 설정 **버퍼 크기** 설정 대화 상자에서.|  
|MAXSCANROWS|기존 데이터를 기반으로 하는 열의 데이터 형식을 설정 하는 경우 검색할 행의 수입니다.<br /><br /> 검색할 행에 대해 1에서 16 사이의 숫자로 입력할 수 있습니다. 기본값은 8입니다. 0으로 설정 하는 경우 모든 행 검사 됩니다. (제한 벗어나는 숫자로 오류가 반환 됩니다.)<br /><br /> 동일한 옵션을 설정 **검색할 행** 설정 대화 상자에서.|  
|PAGETIMEOUT|(밀리초) (사용 되지 않음) 하는 경우 페이지를 제거 하기 전에 버퍼에 남아 있는 기간을 지정 합니다. 기본값은 5-1/10 초 (0.5 초). 이 옵션은 ODBC 드라이버를 사용 하는 모든 데이터 원본에 적용 됩니다 note 합니다.<br /><br /> 동일한 옵션을 설정 **페이지 시간 제한** 설정 대화 상자에서.|  
|PWD|암호입니다.|  
|READONLY|읽기 전용 파일을 확인. 읽기 전용 파일을 만들기 위해 FALSE입니다.<br /><br /> 동일한 옵션을 설정 **읽기 전용** 설정 대화 상자에서.|  
|REPAIR_DB|커밋 프로세스 동안 발생 하는 오류로 인해 손상 된 데이터베이스를 복구 합니다.<br /><br /> DSN 키워드를 사용 하 여 동일한 문에서 REPAIR_DB 키워드를 사용 하는 경우이 드라이버는 DSN 키워드를 무시 합니다. 따라서 데이터베이스를 복구 하 고 DSN을 지정 하는 두 단계로 이루어집니다.|  
|SYSTEMDB|Microsoft Access 드라이버의 경우 시스템 데이터베이스 파일에 경로 지정 합니다.<br /><br /> 동일한 옵션을 설정 **시스템 데이터베이스** 설정 대화 상자에서.|  
|스레드|사용 하도록 엔진에 대 한 백그라운드 스레드의 수입니다. 이 값을 3으로 기본적으로 사용 되지만 변경할 수 있습니다.<br /><br /> 동일한 옵션을 설정 **스레드** 설정 대화 상자에서.|  
|UID|Microsoft Access 드라이버에 대 한 사용자 ID 이름 로그인에 사용 합니다.|  
|USERCOMMITSYNC|Microsoft Access 드라이버를 사용자 정의 트랜잭션을 비동기적으로 수행 하는지 여부를 결정 합니다. 이 값은 처음에 Microsoft Access 드라이버를 완료 하는 사용자 정의 트랜잭션 커밋을 대기 함을 의미는 "예"로 설정 됩니다.<br /><br /> 그 결과에 신중 하 게 고려 하지 않고이 옵션의 값을 변경할 수 없습니다. 옵션에 대 한 자세한 내용은 참조는 *Microsoft Jet 데이터베이스 엔진 Programmer's Guide*합니다.<br /><br /> 동일한 옵션을 설정 **UserCommitSync** 설정 대화 상자에서.|
