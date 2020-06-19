---
title: SqlLocalDB 유틸리티 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
helpviewer_keywords:
- SqlLocalDB utility [SQL Server]
- local database runtime utility
- LocalDB, SqlLocalDB Utility
ms.assetid: d785cdb7-1ea0-4871-bde9-1ae7881190f5
author: stevestein
ms.author: sstein
ms.openlocfilehash: 168a343c208c7b9d98f3f03a802e40488602a7d0
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85007067"
---
# <a name="sqllocaldb-utility"></a>SqlLocalDB 유틸리티
  유틸리티를 사용 `SqlLocalDB` 하 여 LocalDB의 인스턴스를 만듭니다 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssExpCurrent](../includes/ssexpcurrent-md.md)] **LocalDB**. `SqlLocalDB`유틸리티 (SqlLocalDB.exe)는 사용자와 개발자가 LocalDB의 인스턴스를 만들고 관리 하는 데 사용할 수 있는 간단한 명령줄 도구입니다 [!INCLUDE[ssExpress](../includes/ssexpress-md.md)] **LocalDB**. **Localdb**를 사용 하는 방법에 대 한 자세한 내용은 [SQL Server 2014 Express LocalDB](../database-engine/configure-windows/sql-server-2016-express-localdb.md)를 참조 하세요.  
  
## <a name="syntax"></a>구문  
  
```  
SqlLocalDB.exe   
{  
      [ create   | c ] <instance-name><instance-version> [-s ]  
    | [ delete   | d ] <instance-name>  
    | [ start    | s ] <instance-name>  
    | [ stop     | p ] <instance-name>  [ -i ] [ -k ]  
    | [ share    | h ] ["<user_SID>" | "<user_account>" ] "<private-name>""<shared-name>"  
    | [ unshare  | u ] "<shared-name>"  
    | [ info     | i ] <instance-name>  
    | [ versions | v ]  
    | [ trace    | t ] [ on | off ]  
    | [ help     | -? ]  
}  
```  
  
## <a name="arguments"></a>인수  
 [ **만들기**  |  **c** ] *\<instance-name>* *\<instance-version>* [**-s** ]  
 [!INCLUDE[ssExpress](../includes/ssexpress-md.md)]**LocalDB**의 새 인스턴스를 만듭니다. `SqlLocalDB`는 [!INCLUDE[ssExpress](../includes/ssexpress-md.md)] 인수로 지정 된 이진 파일의 버전을 사용 *\<instance-version>* 합니다. 버전 번호는 하나 이상의 숫자를 포함하는 숫자 형식으로 지정됩니다. 부 버전 번호(서비스 팩)는 선택 사항입니다. 예를 들어 버전 번호 11.0 또는 11.0.1186은 모두 허용됩니다. 지정된 버전을 컴퓨터에 설치해야 합니다. 지정 하지 않으면 버전 번호는 기본적으로 유틸리티 버전으로 지정 `SqlLocalDB` 됩니다. **–s**를 추가하여 **LocalDB**의 새 인스턴스를 시작합니다.  
  
 [ **share** | **h** ]  
 지정한 공유 이름을 사용하여 지정한 프라이빗 **LocalDB** 인스턴스를 공유합니다. 사용자 SID 또는 계정 이름을 생략하면 기본값으로 현재 사용자가 사용됩니다.  
  
 [ **unshared** | **u** ]  
 **LocalDB**의 지정된 공유 인스턴스의 공유를 중지합니다.  
  
 [ **삭제**  |  **d** ]*\<instance-name>*  
 [!INCLUDE[ssExpress](../includes/ssexpress-md.md)]**LocalDB**의 지정된 인스턴스를 삭제합니다.  
  
 [ **시작**  |  **s** ] " *\<instance-name>* "  
 [!INCLUDE[ssExpress](../includes/ssexpress-md.md)]**LocalDB**의 지정된 인스턴스를 시작합니다. 성공하면 문이 **LocalDB**의 명명된 파이프 주소를 반환합니다.  
  
 [ **중지**  |  **p** ] *\<instance-name>* [**-i** ] [**-k** ]  
 [!INCLUDE[ssExpress](../includes/ssexpress-md.md)]**LocalDB**의 지정된 인스턴스를 중지합니다. **-I** 를 추가 하면 옵션을 사용 하 여 인스턴스 종료를 요청 합니다 `NOWAIT` . **–k**를 추가하면 인스턴스 프로세스에 연결하지 않고 해당 프로세스를 중지합니다.  
  
 [ **정보**  |  **i** ] [ *\<instance-name>* ]  
 현재 사용자가 소유한 [!INCLUDE[ssExpress](../includes/ssexpress-md.md)]**LocalDB** 의 모든 인스턴스를 나열합니다.  
  
 *\<instance-name>* 지정 된 localdb 인스턴스의 이름, 버전, 상태 (실행 중 또는 중지 됨), 마지막 시작 시간 [!INCLUDE[ssExpress](../includes/ssexpress-md.md)] **LocalDB**및 **localdb**의 로컬 파이프 이름을 반환 합니다.  
  
 [ **trace** | **t** ] **on** | **off**  
 **trace on** 을 사용 하면 `SqlLocalDB` 현재 사용자에 대 한 API 호출을 추적할 수 있습니다. **trace off** 를 사용하면 추적이 사용되지 않습니다.  
  
 **-?**  
 각 옵션에 대 한 간략 한 설명을 반환 `SqlLocalDB` 합니다.  
  
## <a name="remarks"></a>설명  
 *instance name* 인수는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 식별자에 대한 규칙을 따르거나 큰따옴표로 묶어야 합니다.  
  
 인수 없이 SqlLocalDB를 실행하면 도움말 텍스트가 반환됩니다.  
  
 시작 이외의 작업은 현재 로그인한 사용자에 속하는 인스턴스에 대해서만 수행할 수 있습니다.  
  
## <a name="examples"></a>예제  
  
### <a name="a-creating-an-instance-of-localdb"></a>A. LocalDB의 인스턴스 만들기  
 다음 예에서는 [!INCLUDE[ssExpress](../includes/ssexpress-md.md)]**바이너리를 사용하여** 라는 `DEPARTMENT` LocalDB [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 의 인스턴스를 만든 다음 인스턴스를 시작합니다.  
  
```  
SqlLocalDB.exe create "DEPARTMENT" 12.0 -s  
```  
  
### <a name="b-working-with-a-shared-instance-of-localdb"></a>B. LocalDB의 공유 인스턴스 작업  
 관리자 권한을 사용하여 명령 프롬프트를 엽니다.  
  
```  
SqlLocalDB.exe create "DeptLocalDB"  
SqlLocalDB.exe share "DeptLocalDB" "DeptSharedLocalDB"  
SqlLocalDB.exe start "DeptLocalDB"  
SqlLocalDB.exe info "DeptLocalDB"  
REM The previous statement outputs the Instance pipe name for the next step  
sqlcmd -S np:\\.\pipe\LOCALDB#<use your pipe name>\tsql\query  
CREATE LOGIN NewLogin WITH PASSWORD = 'Passw0rd!!@52';   
GO  
CREATE USER NewLogin;  
GO  
EXIT  
```  
  
 다음 코드를 실행해서 **로그인을 사용하여** LocalDB `NewLogin` 의 공유 인스턴스에 연결합니다.  
  
```  
sqlcmd -S (localdb)\.\DeptSharedLocalDB -U NewLogin -P Passw0rd!!@52  
```  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server 2014 Express LocalDB](../database-engine/configure-windows/sql-server-2016-express-localdb.md)  
  
  
