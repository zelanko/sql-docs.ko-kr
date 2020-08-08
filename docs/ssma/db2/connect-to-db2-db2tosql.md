---
title: D b 2에 연결 (DB2ToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 9d485fd0-ab5d-402a-a59a-e9982a61b7de
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 7180e78e7ec34e9c75d25dac51101e28291b1f4c
ms.sourcegitcommit: e8f6c51d4702c0046aec1394109bc0503ca182f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/07/2020
ms.locfileid: "87933846"
---
# <a name="connect-to-db2-db2tosql"></a>D b 2에 연결 (DB2ToSQL)
**Db2에 연결** 대화 상자를 사용 하 여 마이그레이션할 db2 데이터베이스에 연결 합니다.  
  
이 대화 상자에 액세스 하려면 **파일** 메뉴에서 **DB2에 연결**을 선택 합니다. 이전에 연결한 경우 명령은 d b 2 **에 다시 연결**됩니다.  
  
## <a name="options"></a>옵션  
**공급 기업**  
DB2 데이터베이스에 연결 하기 위한 데이터 액세스 공급자를 선택 합니다. 사용 가능한 공급자는 DB2 클라이언트 공급자와 OLE DB 공급자입니다. 기본값은 DB2 클라이언트 공급자입니다.  
  
**모드**  
표준, TNSNAME 또는 연결 문자열 모드 중 하나를 선택 합니다.  
  
-   표준 모드에서는 공급자, 서버 이름, 서버 포트, DB2 SID, 사용자 이름 및 암호에 대 한 값을 입력 하거나 선택 합니다.  
  
-   TNSNAME 모드에서 DB2 데이터베이스, 사용자 이름 및 암호의 연결 식별자 (TNS alias)를 입력 합니다.  
  
-   연결 문자열 모드에서는 연결 문자열을 제공 합니다.  
  
    > [!IMPORTANT]  
    > 연결 문자열 모드를 사용 하는 것은 좋지 않습니다. 텍스트에 암호가 포함 될 수 있으며 일반 텍스트로 전송 되기 때문입니다.  
  
기본값은 표준 모드입니다.  
  
**서버 이름**  
DB2 서버 이름을 입력 합니다. 기본 서버 이름은 컴퓨터 이름과 동일 합니다. 표준 모드 옵션입니다.  
  
**서버 포트**  
DB2에 연결 하는 데 1521 (기본값) 이외의 포트 번호를 사용 하는 경우 포트 번호를 입력 합니다. 표준 모드 옵션입니다.  
  
**연결 식별자**  
DB2 연결 식별자를 입력 합니다. 로컬 tnsnames. ora 파일에 정의 된 데이터베이스의 별칭입니다.  
  
TNSNAME 모드 옵션입니다.  
  
**DB2 SID**  
데이터베이스에 대 한 SID를 입력 합니다. SID는 컴퓨터에서 DB2 데이터베이스를 구별 하는 식별자입니다. 데이터베이스의 기본 SID는 데이터베이스 이름의 처음 8 자입니다.  
  
표준 모드 옵션입니다.  
  
**사용자 이름**  
SSMA에서 DB2 데이터베이스에 연결 하는 데 사용할 사용자 이름을 입력 합니다.  
  
**암호**  
사용자 이름에 대한 암호를 입력합니다.  
  
**연결 문자열**  
> [!IMPORTANT]  
> 연결 문자열 모드를 사용 하는 것은 좋지 않습니다. 텍스트에 암호가 포함 될 수 있으며 일반 텍스트로 전송 되기 때문입니다.  
  
연결 문자열 모드를 사용 하는 경우 DB2 연결에 대 한 전체 연결 문자열을 입력 합니다.  
  
연결 문자열은 매개 변수 이름 및 값 쌍으로 구성 됩니다.  
  
-   OLE DB 연결 문자열 정보는 MSDN Library에서 [Microsoft OLE DB Provider for DB2](https://go.microsoft.com/fwlink/?LinkId=85640) 문서를 참조 하세요.  
  
SSMA 연결 문자열의 경우 항상 Provider 매개 변수를 포함 합니다. 또한 DB2에 연결할 때 Port 매개 변수를 포함 해야 합니다.  
  
