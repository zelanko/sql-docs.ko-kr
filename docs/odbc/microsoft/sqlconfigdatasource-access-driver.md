---
title: SQLConfigDataSource (액세스 드라이버) | 마이크로 소프트 문서
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
ms.openlocfilehash: 48668525b578845fc330881d7c7de503d69d0928
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81284053"
---
# <a name="sqlconfigdatasource-access-driver"></a>SQLConfigDataSource(Access 드라이버)
> [!NOTE]  
>  이 항목에서는 액세스 드라이버 관련 정보를 제공합니다. 이 함수에 대한 일반적인 정보는 [ODBC API 참조](../../odbc/reference/syntax/odbc-api-reference.md)에서 적절한 항목을 참조하십시오.  
  
 데이터 원본을 동적으로 추가, 수정 또는 삭제하는 데 사용되는 **SQLConfigDataSource** 함수는 다음 키워드를 사용합니다.  
  
|키워드|설명|  
|-------------|-----------------|  
|콜라팅시퀀스|필드가 정렬되는 시퀀스입니다.<br /><br /> 이렇게 하면 설정 대화 상자에서 **시퀀스 정렬과** 동일한 옵션이 설정됩니다.|  
|COMPACT_DB|데이터베이스 파일에서 데이터 압축을 수행합니다. 다음 형식: COMPACT_DB=<><\<>선택적 ENCRYPT 키워드> optionaL_sort_order path_name.<br /><br /> DSN 키워드와 동일한 문에서 COMPACT_DB 키워드를 사용하는 경우 이 드라이버는 DSN 키워드를 무시합니다. 따라서 데이터베이스를 압축하고 DSN을 지정하는 것은 2단계 프로세스입니다.|  
|CREATE_DB|데이터베이스 파일을 만듭니다. 다음 형식: CREATE_DB= optional_ENCRYPT \<optional_sort><path_name path_name><><><><> 경로 이름은 Microsoft Access 데이터베이스의 전체 경로입니다. 경로 이름이 기존 데이터베이스를 지정하면 오류가 반환됩니다. 정렬 순서는 Microsoft 액세스 설정 대화 상자에서 만들기 단추를 누를 때 표시되는 새 데이터베이스 대화 상자에 설정된 대로 설정됩니다. 정렬 순서를 지정하지 않으면 일반이 사용됩니다.<br /><br /> DSN 키워드와 동일한 문에서 CREATE_DB 키워드를 사용하는 경우 이 드라이버는 DSN 키워드를 무시합니다. 따라서 데이터베이스를 만들고 DSN을 지정하는 것은 2단계 프로세스입니다. CREATE_DB 키워드를 사용하는 경우 만들 Microsoft Access 데이터베이스의 pathname에 하나 이상의 공백이 포함되어 있는 경우 다음 예제와 같이 전체 경로 이름을 이중 따옴표로 묶어야 합니다.<br /><br /> "C:\프로그램 파일\일반 파일\ MyAccess.mdb"<br /><br /> "C:\프로그램 파일\Access2.mdb"<br /><br /> CREATE_DB=C:\TEMP\test.mdb(따옴표 필요 없음)|  
|CREATE_SYSDB|시스템 데이터베이스 파일을 만듭니다. 다음 형식: CREATE_SYSDB=\<경로 이름 \<>선택적 정렬 순서>, 여기서 경로 이름은 Microsoft Access 데이터베이스에 대 한 전체 경로입니다. 경로 이름이 기존 데이터베이스를 지정하면 오류가 반환됩니다. **ODBC Microsoft 액세스 설정** 대화 상자에서 **만들기** 단추를 클릭하면 새 **데이터베이스** 대화 상자에 정렬 순서가 설정됩니다. 정렬 순서를 지정하지 않으면 일반이 사용됩니다.|  
|CREATE_V2DB|Microsoft Access 2.0과 호환되는 데이터베이스 파일을 만듭니다. 다음 형식: CREATE_V2DB=\<경로 이름 \<>선택적 정렬 순서>, 여기서 경로 이름은 Microsoft Access 데이터베이스에 대 한 전체 경로입니다. 경로 이름이 기존 데이터베이스를 지정하면 오류가 반환됩니다. 정렬 순서는 Microsoft 액세스 설정 대화 상자에서 만들기 단추를 누를 때 표시되는 새 데이터베이스 대화 상자에 설정된 대로 설정됩니다. 정렬 순서를 지정하지 않으면 일반이 사용됩니다.<br /><br /> DSN 키워드와 동일한 문에서 CREATE_V2DB 키워드를 사용하는 경우 이 드라이버는 DSN 키워드를 무시합니다. 따라서 데이터베이스를 만들고 DSN을 지정하는 것은 2단계 프로세스입니다.<br /><br /> CREATE_V2DB 키워드를 사용하는 경우 만들 Microsoft Access 데이터베이스의 pathname에 하나 이상의 공백이 포함되어 있는 경우 다음 예제와 같이 전체 경로 이름을 이중 따옴표로 묶어야 합니다.<br /><br /> "C:\프로그램 파일\일반 파일\ MyAccess.mdb"<br /><br /> "C:\프로그램 파일\Access2.mdb"<br /><br /> CREATE_V2DB =C:\TEMP\test.mdb(따옴표 필요 없음)|  
|DBQ|데이터베이스 파일의 이름입니다.<br /><br /> 이렇게 하면 설정 대화 상자의 **데이터베이스와** 동일한 옵션이 설정됩니다.|  
|기본디더|데이터베이스 파일에 대한 경로 사양입니다.|  
|설명|데이터 원본의 데이터에 대한 설명입니다.<br /><br /> 이렇게 하면 설정 대화 상자의 **설명과** 동일한 옵션이 설정됩니다.|  
|DRIVER|드라이버 DLL에 대한 경로 사양입니다.|  
|드라이버 ID|드라이버에 대한 정수 ID입니다.  25 (마이크로소프트 액세스)|  
|Fil|마이크로 소프트 액세스에 대한 파일 형식 MS 액세스|  
|암시적 커밋싱크|Microsoft Access 드라이버가 비동기적으로 내부 커밋을 수행할지 또는 암시적 커밋을 수행할지 여부를 결정합니다. 이 값은 처음에 "예"로 설정되어 있으며, 이는 Microsoft Access 드라이버가 내부/암시적 트랜잭션의 커밋이 완료될 때까지 기다립니다.<br /><br /> 이 옵션의 값은 결과를 신중하게 고려하지 않고 변경해서는 안 됩니다. 이 옵션에 대한 자세한 내용은 *Microsoft Jet 데이터베이스 엔진 프로그래머 가이드를*참조하십시오.<br /><br /> 이렇게 하면 설치 대화 상자에서 **ImplicitCommitSync와** 동일한 옵션이 설정됩니다.|  
|Maxbuffersize|Microsoft Access에서 디스크로 데이터를 전송하는 데 사용되는 내부 버퍼의 크기(킬로바이트)입니다. 기본 버퍼 크기는 2048KB(2048로 표시)입니다. 256으로 나눌 수 있는 모든 정수 값을 사용할 수 있습니다. 이렇게 하면 설정 대화 상자에서 **버퍼 크기와** 동일한 옵션이 설정됩니다.|  
|맥스칸로우스|기존 데이터를 기반으로 열의 데이터 형식을 설정할 때 검색할 행 수입니다.<br /><br /> 행을 스캔하려면 1에서 16까지의 숫자를 입력할 수 있습니다. 값은 기본값은 8입니다. 0으로 설정하면 모든 행이 검색됩니다. (한계를 벗어난 숫자는 오류를 반환합니다.)<br /><br /> 이렇게 하면 설정 대화 상자에서 **검색할 행과** 동일한 옵션이 설정됩니다.|  
|페이지 시간 시간|페이지(사용하지 않은 경우)가 제거되기 전에 버퍼에 남아 있는 기간을 밀리초 단위로 지정합니다. 기본값은 1초의 5/10(0.5초)입니다. 이 옵션은 ODBC 드라이버를 사용하는 모든 데이터 원본에 적용됩니다.<br /><br /> 이렇게 하면 설정 대화 상자에서 **페이지 시간 설정과** 동일한 옵션이 설정됩니다.|  
|PWD|암호입니다.|  
|READONLY|TRUE는 파일을 읽기 전용으로 만듭니다. FALSE파일을 읽기 전용으로 만들지 않도록 합니다.<br /><br /> 이렇게 하면 설정 대화 상자에서 **만 읽기와** 동일한 옵션이 설정됩니다.|  
|REPAIR_DB|커밋 프로세스 중에 발생하는 오류로 인해 손상된 데이터베이스를 복구합니다.<br /><br /> DSN 키워드와 동일한 문에서 REPAIR_DB 키워드를 사용하는 경우 이 드라이버는 DSN 키워드를 무시합니다. 따라서 데이터베이스를 복구하고 DSN을 지정하는 것은 2단계 프로세스입니다.|  
|시스템 DB|Microsoft Access 드라이버의 경우 시스템 데이터베이스 파일에 대한 경로 사양입니다.<br /><br /> 이렇게 하면 설정 대화 상자에서 **시스템 데이터베이스와** 동일한 옵션이 설정됩니다.|  
|스레드|사용할 엔진의 배경 스레드 수입니다. 이 값은 기본값은 3이지만 변경할 수 있습니다.<br /><br /> 이렇게 하면 설정 대화 상자의 스레드와 동일한 옵션이 **설정됩니다.**|  
|UID|Microsoft Access 드라이버의 경우 로그인에 사용되는 사용자 ID 이름입니다.|  
|사용자 커밋싱크|Microsoft Access 드라이버가 사용자 정의 트랜잭션을 비동기적으로 수행할지 여부를 결정합니다. 이 값은 처음에 "예"로 설정되어 있으며, 이는 Microsoft Access 드라이버가 사용자 정의 트랜잭션의 커밋이 완료될 때까지 기다립니다.<br /><br /> 이 옵션의 값은 결과를 신중하게 고려하지 않고 변경해서는 안 됩니다. 이 옵션에 대한 자세한 내용은 *Microsoft Jet 데이터베이스 엔진 프로그래머 가이드를*참조하십시오.<br /><br /> 이렇게 하면 설치 대화 상자에서 **UserCommitSync와** 동일한 옵션이 설정됩니다.|
