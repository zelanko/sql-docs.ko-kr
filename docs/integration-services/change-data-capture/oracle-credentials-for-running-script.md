---
description: 스크립트 실행을 위한 Oracle 자격 증명
title: 스크립트 실행을 위한 Oracle 자격 증명 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 4a301cb0-2f5b-41ba-81bf-46b41d07f137
author: chugugrace
ms.author: chugu
ms.openlocfilehash: ba5959cec249da89655d1edb4df8ef8ca225a416
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88426015"
---
# <a name="oracle-credentials-for-running-script"></a>스크립트 실행을 위한 Oracle 자격 증명

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  Oracle CDC Designer 콘솔에서 Oracle 보완 로깅 스크립트를 실행하면 스크립트를 실행 중인 Oracle 사용자의 자격 증명을 묻는 메시지가 표시됩니다. 이 스크립트를 실행하려면 캡처할 모든 테이블에 대한 ALTER TABLE 권한과 DBA_LOG_GROUPS 뷰에 대한 SELECT 권한이 Oracle 사용자에게 있어야 합니다.  
  
## <a name="task-list"></a>작업 목록  
 이 대화 상자에 다음을 입력합니다.  
  
 **인증**  
  
 다음 중 하나를 선택합니다.  
  
-   **Windows 인증**: 현재 Windows 도메인 자격 증명을 사용하려면 선택합니다. Windows 인증을 사용하도록 Oracle 데이터베이스를 구성한 경우에만 이 옵션을 사용할 수 있습니다.  
  
-   **Oracle 인증**: 이 옵션을 선택하는 경우 연결 중인 원본 Oracle 데이터베이스에 사용자의 **사용자 이름** 과 **암호** 를 입력해야 합니다.  
  
## <a name="see-also"></a>관련 항목  
 [How to Manage a CDC Instance](../../integration-services/change-data-capture/how-to-manage-a-cdc-instance.md)   
 [보완 로깅 스크립트 검토 및 생성](../../integration-services/change-data-capture/review-and-generate-supplemental-logging-scripts.md)  
  
  
