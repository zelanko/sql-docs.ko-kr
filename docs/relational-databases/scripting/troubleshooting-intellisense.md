---
title: IntelliSense 문제 해결(SQL Server Management Studio) | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.technology: scripting
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- unavailable options [IntelliSense]
- IntelliSense [SQL Server], troubleshooting
- IntelliSense [SQL Server], unavailable options
- troubleshooting [IntelliSense]
ms.assetid: 4b72ffc6-aea2-4e11-ab36-fa2de4d7bcc5
caps.latest.revision: 41
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 6dbbe26d5e6c03f1e7e85ae53ce751a6aac4b3c5
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43065755"
---
# <a name="troubleshooting-intellisense"></a>문제 해결 IntelliSense
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  다음과 같은 몇몇 경우에서는 IntelliSense 옵션이 제대로 작동하지 않을 수 있습니다.  
  
## <a name="conditions-that-affect-intellisense"></a>IntelliSense에 영향을 주는 조건  
 IntelliSense 동작에 영향을 줄 수 있는 조건은 다음과 같습니다.  
  
-   커서 위에 코드 오류가 존재합니다.  
  
     삽입 지점 위치 위에 불완전한 문이나 다른 코딩 오류가 있을 경우 IntelliSense는 코드 요소를 구문 분석하지 못할 수 있으며 따라서 작동하지 않게 됩니다. 해당 코드를 주석으로 처리하여 IntelliSense를 다시 사용할 수 있습니다.  
  
-   삽입 지점이 코드 주석 안에 있습니다.  
  
     원본 파일의 주석 안에 삽입 지점이 있을 경우 IntelliSense 옵션을 사용할 수 없습니다.  
  
-   삽입 지점이 문자열 리터럴 안에 있습니다.  
  
     다음과 같이 문자열 리터럴을 둘러싸는 따옴표 안에 삽입 지점이 있을 경우 IntelliSense 옵션을 사용할 수 없습니다.  
  
     `WHERE FirstName LIKE 'Patri%|'`  
  
-   자동 옵션이 해제되었습니다.  
  
     기본적으로 대부분의 IntelliSense 기능은 자동으로 작동하지만 임의의 기능을 해제할 수 있습니다.  
  
     자동 문 완성이 해제된 경우에도 IntelliSense 기능을 사용할 수 있습니다. 자세한 내용은 [IntelliSense 구성&#40;SQL Server Management Studio&#41;](../../relational-databases/scripting/configure-intellisense-sql-server-management-studio.md)을 참조하세요.  
  
## <a name="database-engine-query-intellisense"></a>데이터베이스 엔진 쿼리 IntelliSense  
 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 쿼리 편집기에는 다음과 같은 문제가 적용됩니다.  
  
-   [!INCLUDE[ssDE](../../includes/ssde-md.md)] 쿼리 편집기의 IntelliSense 기능이 일부 [!INCLUDE[tsql](../../includes/tsql-md.md)] 구문 요소를 지원하지 않습니다. 매개 변수 도움말은 일부 개체에서 확장 저장 프로시저와 같은 매개 변수를 지원하지 않습니다. 자세한 내용은 [IntelliSense에서 지원되는 Transact-SQL 구문](../../relational-databases/scripting/transact-sql-syntax-supported-by-intellisense.md)을 참조하세요.  
  
-   [!INCLUDE[ssDE](../../includes/ssde-md.md)] 쿼리 편집기가 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 이상의 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 인스턴스에 연결되는 경우에만 IntelliSense를 사용할 수 있습니다. 쿼리 편집기가 이전 버전의 [!INCLUDE[ssDE](../../includes/ssde-md.md)]에 연결되는 경우에는 IntelliSense를 사용할 수 없습니다.  
  
-   SQLCMD 모드를 설정하면 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 쿼리 편집기에서 IntelliSense가 해제됩니다.  
  
-   IntelliSense 기능은 편집기 창이 데이터베이스에 연결된 후 다른 연결에서 만든 데이터베이스 개체를 처리하지 않습니다. 개체가 완성 목록과 같은 IntelliSense 기능에서 누락되어 있는 경우 다음 세 가지 메커니즘 중 하나를 선택하여 편집기 창의 개체 캐시를 새로 고칠 수 있습니다.  
  
    -   **편집** 메뉴를 선택하고 **IntelliSense**를 선택한 다음 **로컬 캐시 새로 고침**을 선택합니다.  
  
    -   바로 가기 키 Ctrl+Shift+R을 사용합니다.  
  
    -   [!INCLUDE[ssDE](../../includes/ssde-md.md)] 인스턴스에서 편집기 창의 연결을 끊은 후 다시 연결합니다.  
  
-   사용자가 권한을 가지고 있지 않은 데이터베이스 개체는 완성 목록에 포함되지 않습니다. IntelliSense 플래그는 사용자가 권한을 가지고 있는 개체를 참조합니다. 예를 들어 다른 사용자가 작성한 스크립트를 열면 스크립트 작성한 사용자만 권한을 가지고 있고 사용자 자신은 권한을 가지고 있지 않은 개체에 대한 모든 참조는 올바르지 않은 것으로 플래그가 지정됩니다.  
  
-   [!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스와의 연결이 끊어지면 완성 목록이 작동하지 않을 수 있습니다. 인스턴스에 다시 연결하십시오.  
  
  
