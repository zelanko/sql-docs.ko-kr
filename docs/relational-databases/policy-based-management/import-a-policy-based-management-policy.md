---
description: 정책 기반 관리 정책 가져오기
title: 정책 기반 관리 정책 가져오기 | Microsoft 문서
ms.custom: ''
ms.date: 08/06/2020
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Policy-Based Management, import policy
ms.assetid: 850b7ef9-d2b7-4754-bf04-7cb419ffb776
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 1ea5d3c83667dbd194e9fb82ae7bce2e815d479b
ms.sourcegitcommit: 27f95e50f11a98164e9e7a5130a3e00ac06b4cea
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/28/2020
ms.locfileid: "91412774"
---
# <a name="import-a-policy-based-management-policy"></a>정책 기반 관리 정책 가져오기
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  이 항목에서는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 를 사용하여 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 정책 기반 관리 정책 인스턴스를 가져오는 방법에 대해 설명합니다.  
  
## <a name="permissions"></a>사용 권한
 msdb 데이터베이스에서 PolicyAdministratorRole 역할의 멤버 자격이 필요합니다.

  
##  <a name="using-sql-server-management-studio"></a>SQL Server Management Studio 사용  
  
### <a name="to-import-a-policy-instance"></a>정책 인스턴스를 가져오려면  
  
1.  **개체 탐색기**에서 더하기 기호를 클릭하여 새로 가져온 정책 인스턴스가 상주할 서버를 확장합니다.  
  
2.  더하기 기호를 클릭하여 **관리** 폴더를 확장합니다.  
  
3.  더하기 기호를 클릭하여 **정책 관리**를 확장합니다.  
  
4.  **정책** 폴더를 마우스 오른쪽 단추로 클릭하고 **정책 가져오기**를 선택합니다.  
  
5.  **가져오기** 대화 상자에서 파일의 경로와 이름을 입력하거나 찾아보기(**...**) 단추를 사용하여 정책이 포함된 XML 파일을 찾은 다음 파일을 선택합니다. **가져오기** 대화 상자에서 사용할 수 있는 옵션에 대한 자세한 내용은 [Import Policies Dialog Box](../../relational-databases/policy-based-management/import-policies-dialog-box.md)를 참조하세요.  
  
6.  완료되었으면 **확인**을 클릭합니다.  


## <a name="example-policies"></a>예제 정책
 예제 정책은 [SQL Server 샘플 코드 리포지토리](https://github.com/microsoft/sql-server-samples/tree/master/samples/features/epm-framework/sample-policies)에서 사용할 수 있습니다. 이 정책은 사용 중인 정책 기반 관리 정책의 기준으로 가져와 사용할 수 있습니다.
