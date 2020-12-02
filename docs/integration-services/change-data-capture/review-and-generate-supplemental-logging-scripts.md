---
description: 보완 로깅 스크립트 검토 및 생성
title: 보완 로깅 스크립트 검토 및 생성 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- scripts
ms.assetid: 5c858ae2-37d6-42e8-a252-7f6ed4e628a7
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 77a6b4f11ea2e01f43f1be335fad893ee87f1e90
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/26/2020
ms.locfileid: "88457688"
---
# <a name="review-and-generate-supplemental-logging-scripts"></a>보완 로깅 스크립트 검토 및 생성

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  **스크립트** 탭을 사용하여 보완 로깅을 설정하는 Oracle 원본 데이터베이스에서 스크립트를 실행하거나 다시 실행할 수 있습니다.  
  
 스크립트를 실행하기 전에 다음 중 하나를 선택하십시오.  
  
 **이 세션에 변경 내용 포함**  
 CDC 인스턴스에 추가된 새 테이블 또는 속성 편집기를 사용하여 변경한 테이블에서 스크립트를 실행하려면 선택합니다.  
  
> [!NOTE]  
>  CDC 인스턴스에서 테이블이 변경되지 않은 경우 Oracle 보완 로깅 스크립트 영역이 비어 있습니다.  
  
 **모든 테이블/캡처 인스턴스 포함**  
 CDC 인스턴스의 모든 테이블 및 캡처 인스턴스에 대해 스크립트를 실행하려면 선택합니다.  
  
 이러한 옵션 중 하나를 선택 후 보완 로깅 스크립트를 실행합니다.  
  
### <a name="to-run-the-supplemental-logging-scripts"></a>보완 로깅 스크립트를 실행하려면  
  
1.  **스크립트 실행** 을 클릭하여 CDC 인스턴스에 대해 정의된 테이블에서 보완 로깅 스크립트를 실행합니다. 이 스크립트는 캡처된 테이블에 업데이트 작업을 로깅할 때 트랜잭션 로그에 모든 관련 열을 쓰도록 Oracle 데이터베이스에 지시합니다. 이 스크립트는 일반적으로 Oracle 시스템 관리자가 검사하고 실행합니다.  
  
2.  보완 로깅 스크립트를 실행하면 유효한 Oracle 사용자 이름과 암호를 입력할 수 있는 스크립트 실행을 위한 Oracle 자격 증명 대화 상자가 열립니다. 적절한 Oracle 자격 증명을 제공하는 방법은 [Oracle Credentials for Running Script](../../integration-services/change-data-capture/oracle-credentials-for-running-script.md)을 참조하십시오.  
  
 필요한 경우 SQL\*Plus를 사용하여 스크립트를 수동으로 실행할 수도 있습니다.  
  
### <a name="to-run-the-scripts-manually"></a>스크립트를 수동으로 실행하려면  
  
1.  **복사** 를 클릭하여 스크립트를 클립보드에 붙여 넣습니다. SQL* Plus를 열고 Oracle 원본 데이터베이스가 들어 있는 디렉터리로 이동합니다. 스크립트를 SQL\*Plus에 붙여넣어서 실행합니다.  
  
### <a name="to-save-the-supplemental-logging-script-in-a-text-file"></a>텍스트 파일에 보완 로깅 스크립트를 저장하려면  
  
1.  **다른 이름으로 저장** 을 클릭하고 파일을 저장할 위치로 찾습니다.  
  
2.  파일 이름을 지정하고 **저장** 을 클릭하여 파일을 저장합니다.  
  
## <a name="see-also"></a>참고 항목  
 [CDC 인스턴스 속성을 편집하는 방법](../../integration-services/change-data-capture/how-to-edit-the-cdc-instance-properties.md)   
 [스크립트 실행을 위한 Oracle 자격 증명](../../integration-services/change-data-capture/oracle-credentials-for-running-script.md)  
  
  
