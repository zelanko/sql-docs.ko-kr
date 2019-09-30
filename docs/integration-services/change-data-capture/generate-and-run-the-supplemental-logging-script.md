---
title: 보완 로깅 스크립트 생성 및 실행 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- supLog
ms.assetid: 6e940d93-12c6-4cda-9333-5489b245f0e4
author: chugugrace
ms.author: chugu
ms.openlocfilehash: ebf080b38e618a807ff9b3b48711ee89f0e56028
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/26/2019
ms.locfileid: "71298742"
---
# <a name="generate-and-run-the-supplemental-logging-script"></a>보완 로깅 스크립트 생성 및 실행

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  변경 사항을 캡처하기 위한 테이블 선택 페이지를 사용하여 보완 로깅을 설정할 Oracle 원본 데이터베이스에서 스크립트를 실행할 수 있습니다.  
  
 **보완 로깅 스크립트를 실행하려면**  
  
 **스크립트 실행** 을 클릭하여 CDC 인스턴스에 대해 정의된 테이블에서 보완 로깅 스크립트를 실행합니다. 이 스크립트는 캡처된 테이블에 업데이트 작업을 로깅할 때 트랜잭션 로그에 모든 관련 열을 쓰도록 Oracle 데이터베이스에 지시합니다. 이 스크립트는 일반적으로 Oracle 시스템 관리자가 검사하고 실행합니다.  
  
 SQL * Plus를 사용하여 스크립트를 수동으로 실행할 수도 있습니다.  
  
 **스크립트를 수동으로 실행하려면**  
  
 **복사** 를 클릭하여 스크립트를 클립보드에 붙여 넣습니다. SQL* Plus를 열고 Oracle 원본 데이터베이스가 들어 있는 디렉터리로 이동합니다. 스크립트를 SQL\*Plus에 붙여넣어서 실행합니다.  
  
 보완 로깅 스크립트를 텍스트 파일로 저장하려면 **다른 이름으로 저장** 을 클릭하고 파일을 저장할 위치를 찾습니다. 파일 이름을 지정하고 **저장** 을 클릭하여 파일을 저장합니다.  
  
 **다음** 을 클릭하여 [Generate Mirror Tables and CDC Capture Instances](../../integration-services/change-data-capture/generate-mirror-tables-and-cdc-capture-instances.md)을 수행합니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server 변경 데이터베이스 인스턴스를 만드는 방법](../../integration-services/change-data-capture/how-to-create-the-sql-server-change-database-instance.md)   
 [보완 로깅 스크립트 검토 및 생성](../../integration-services/change-data-capture/review-and-generate-supplemental-logging-scripts.md)  
  
  
