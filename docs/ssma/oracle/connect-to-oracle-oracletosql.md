---
title: Oracle에 연결 (OracleToSQL) | Microsoft Docs
description: Oracle 데이터베이스에 연결 하 여 Oracle 용 SSMA를 사용 하 여 마이그레이션을 시작 하는 방법을 알아봅니다. Oracle에 연결 대화 상자를 사용 합니다.
authors: nahk-ivanov
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 23a48cb6-ff30-49bb-b4a7-603ebcab336f
ms.author: alexiva
ms.openlocfilehash: 1c69ace09cccd3d87017fef5bae86e3c03a60ad8
ms.sourcegitcommit: 38639b67a135ca1a50a8e38fa61a089efe90e3f1
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/05/2020
ms.locfileid: "84454526"
---
# <a name="connect-to-oracle-oracletosql"></a>Oracle에 연결 (OracleToSQL)

**Oracle에 연결** 대화 상자를 사용 하 여 마이그레이션하려는 oracle 데이터베이스에 연결 합니다.

이 대화 상자에 액세스 하려면 **파일** 메뉴에서 **Oracle에 연결**을 선택 합니다. 이전에 연결한 경우 명령은 **Oracle에 다시 연결**됩니다.

## <a name="options"></a>옵션

**공급자**  
Oracle 데이터베이스에 연결 하기 위한 데이터 액세스 공급자를 선택 합니다. 사용 가능한 공급자는 Oracle 클라이언트 공급자와 OLE DB 공급자입니다. 기본값은 Oracle 클라이언트 공급자입니다.

**모드**  
표준, TNSNAME 또는 연결 문자열 모드 중 하나를 선택 합니다.

- 표준 모드에서는 공급자, 서버 이름, 서버 포트, Oracle SID, 사용자 이름 및 암호에 대 한 값을 입력 하거나 선택 합니다.
- TNSNAME 모드에서 Oracle 데이터베이스, 사용자 이름 및 암호의 연결 식별자 (TNS alias)를 입력 합니다.
- 연결 문자열 모드에서는 연결 문자열을 제공 합니다.

  > [!IMPORTANT]
  > 연결 문자열 모드를 사용 하는 것은 좋지 않습니다. 텍스트에 암호가 포함 될 수 있으며 일반 텍스트로 전송 되기 때문입니다.

기본값은 표준 모드입니다.

**서버 이름**  
Oracle 서버 이름을 입력 합니다. 기본 서버 이름은 컴퓨터 이름과 동일 합니다. 표준 모드 옵션입니다.

**서버 포트**  
Oracle에 연결 하는 데 1521 (기본값) 이외의 포트 번호를 사용 하는 경우 포트 번호를 입력 합니다. 표준 모드 옵션입니다.

**연결 식별자**  
Oracle 연결 식별자를 입력 합니다. 로컬 tnsnames. ora 파일에 정의 된 데이터베이스의 별칭입니다.

TNSNAME 모드 옵션입니다.

**Oracle SID**  
데이터베이스에 대 한 SID를 입력 합니다. SID는 컴퓨터의 Oracle 데이터베이스를 구별 하는 식별자입니다. 데이터베이스의 기본 SID는 데이터베이스 이름의 처음 8 자입니다.

표준 모드 옵션입니다.

**사용자 이름**  
SSMA가 Oracle 데이터베이스에 연결 하는 데 사용할 사용자 이름을 입력 합니다.

**암호**  
사용자 이름에 대한 암호를 입력합니다.

**연결 문자열**  
> [!IMPORTANT]
> 연결 문자열 모드를 사용 하는 것은 좋지 않습니다. 텍스트에 암호가 포함 될 수 있으며 일반 텍스트로 전송 되기 때문입니다.

연결 문자열 모드를 사용 하는 경우 Oracle 연결에 대 한 전체 연결 문자열을 입력 합니다.

연결 문자열은 매개 변수 이름 및 값 쌍으로 구성 됩니다.

- OLE DB 연결 문자열 정보는 MSDN Library에서 [Microsoft OLE DB Provider for Oracle](https://go.microsoft.com/fwlink/?LinkId=85640) 문서를 참조 하세요.

SSMA 연결 문자열의 경우 항상 Provider 매개 변수를 포함 합니다. 또한 Oracle에 연결할 때 Port 매개 변수를 포함 해야 합니다.

## <a name="next-steps"></a>다음 단계

마이그레이션 프로세스의 다음 단계는 [SQL Server에 연결](connect-to-sql-server-oracletosql.md)하는 것입니다.
