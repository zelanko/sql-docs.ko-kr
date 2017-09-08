---
title: "D b 2에 연결 (DB2ToSQL) | Microsoft Docs"
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 9d485fd0-ab5d-402a-a59a-e9982a61b7de
caps.latest.revision: 4
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 733fae47c5c74eb120b7f8719dd53675eb5b7e36
ms.contentlocale: ko-kr
ms.lasthandoff: 08/02/2017

---
# <a name="connect-to-db2-db2tosql"></a>D b 2에 연결 (DB2ToSQL)
사용 하 여는 **d b 2에 연결** 마이그레이션할 DB2 데이터베이스에 연결 하는 대화 상자.  
  
이 대화 상자에 액세스 하는 **파일** 메뉴 선택 **d b 2에 연결**합니다. 이 명령은 이전에 연결한 경우 **d b 2에 다시 연결**합니다.  
  
## <a name="options"></a>옵션  
**공급자**  
DB2 데이터베이스에 연결에 대 한 데이터 액세스 공급자를 선택 합니다. 사용 가능한 공급자는 DB2 클라이언트 공급자 및 OLE DB Provider입니다. 기본값은 DB2 클라이언트 공급자입니다.  
  
**모드**  
Standard, TNSNAME, 또는 연결 문자열 모드를 선택 합니다.  
  
-   표준 모드에서는 입력 하거나 공급자, 서버 이름, 서버 포트, DB2 SID, 사용자 이름 및 암호에 대 한 값을 선택 합니다.  
  
-   TNSNAME 모드에서는 DB2 데이터베이스, 사용자 이름 및 암호의 연결 식별자 (TNS 별칭)을 입력합니다.  
  
-   연결 문자열 모드에서 연결 문자열을 제공 합니다.  
  
    > [!IMPORTANT]  
    > 텍스트 암호에 포함 될 수 있습니다 및 일반 텍스트로 전송 하기 때문에 연결 문자열 모드를 사용 하는 하는 것은 좋지 않습니다.  
  
기본값은 표준 모드.  
  
**서버 이름**  
DB2 서버 이름을 입력 합니다. 기본 서버 이름은 컴퓨터 이름과 같습니다. 표준 모드 옵션입니다.  
  
**서버 포트**  
1521 (기본값) 이외의 포트 번호를 d b 2에 대 한 연결을 사용 하는 경우에 포트 번호를 입력 합니다. 표준 모드 옵션입니다.  
  
**식별자를 연결 합니다.**  
DB2 입력 식별자를 연결 합니다. 이것은 로컬 tnsnames.ora 파일에 정의 된 데이터베이스의 별칭입니다.  
  
TNSNAME 모드 옵션입니다.  
  
**DB2 SID**  
데이터베이스에 대 한 SID를 입력 합니다. SID에는 컴퓨터에서 DB2 데이터베이스를 구별 하는 식별자입니다. 데이터베이스에 대 한 기본 SID는 데이터베이스 이름의 처음 8 자입니다.  
  
표준 모드 옵션입니다.  
  
**사용자 이름**  
SSMA는 DB2 데이터베이스에 연결 하는 데 사용할 사용자 이름을 입력 합니다.  
  
**암호**  
사용자 이름에 대한 암호를 입력합니다.  
  
**연결 문자열**  
> [!IMPORTANT]  
> 텍스트 암호에 포함 될 수 있습니다 및 일반 텍스트로 전송 하기 때문에 연결 문자열 모드를 사용 하는 하는 것은 좋지 않습니다.  
  
연결 문자열 모드를 사용 하는 경우 연결에 대 한 전체 연결 문자열 d b 2를 입력 합니다.  
  
연결 문자열 매개 변수 이름 / 값 쌍으로 구성 됩니다.  
  
-   OLE DB 연결 문자열 정보를 참조 하십시오. [Microsoft OLE DB Provider for d b 2](http://go.microsoft.com/fwlink/?LinkId=85640) MSDN 라이브러리에서 문서.  
  
SSMA 연결 문자열에 대해 항상 Provider 매개 변수를 포함 합니다. D b 2에 연결할 때 포트 매개 변수를 포함 되어 있는지 확인 합니다.  
  

