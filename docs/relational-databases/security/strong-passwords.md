---
title: 강력한 암호 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- logins [SQL Server], passwords
- passwords [SQL Server], strong
- symbols [SQL Server]
- security [SQL Server], passwords
- passwords [SQL Server], symbols
- characters [SQL Server], password policies
- strong passwords [SQL Server]
ms.assetid: 338548f4-c4d8-47ca-b597-5c9c0f2fa205
author: VanMSFT
ms.author: vanto
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 6737a954881a56961b77dcf7d8f0373b0e30e848
ms.sourcegitcommit: 03884a046aded85c7de67ca82a5b5edbf710be92
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/27/2019
ms.locfileid: "74564750"
---
# <a name="strong-passwords"></a>강력한 암호
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
  서버 보안 배포에서 암호는 가장 약한 링크가 될 수 있습니다. 암호를 선택할 때는 항상 주의를 기울여야 합니다. 강력한 암호의 특징은 다음과 같습니다.  
  
-   길이가 적어도 8자 이상입니다.  
  
-   암호는 문자, 숫자 및 기호의 조합입니다.  
  
-   사전에 없는 단어입니다.  
  
-   명령 이름이 아닙니다.  
  
-   사람 이름이 아닙니다.  
  
-   사용자 이름이 아닙니다.  
  
-   컴퓨터 이름이 아닙니다.  
  
-   정기적으로 변경됩니다.  
  
-   이전 암호와 전혀 다른 암호입니다.  
  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 암호는 문자, 기호 및 숫자를 포함하여 최대 128자의 문자를 포함할 수 있습니다. 로그인, 사용자 이름, 역할 및 암호가 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문에서 자주 사용되므로 특정 기호는 큰따옴표(") 또는 대괄호([ ])로 묶어야 합니다. [!INCLUDE[tsql](../../includes/tsql-md.md)] 로그인, 사용자, 역할 또는 암호가 다음에 해당할 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 문에 이러한 구분 기호를 사용하십시오.  
  
-   공백 문자를 포함하거나 공백 문자로 시작하는 경우  
  
-   $ 또는 \@ 문자로 시작하는 경우  
  
 OLE DB 또는 ODBC 연결 문자열에서 사용할 경우 로그인 및 암호는 다음과 같은 문자 [] {}() , ; ?를 포함하지 말아야 함 * ! \@ =. 문자를 포함할 수 없습니다. 이 문자는 연결을 시작하거나 연결 값을 구분하는 데 사용됩니다.  
  
## <a name="related-content"></a>관련 내용  
 [암호 정책](../../relational-databases/security/password-policy.md)  
  
  
