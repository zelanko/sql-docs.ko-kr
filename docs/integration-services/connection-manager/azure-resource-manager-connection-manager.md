---
title: "Azure 리소스 관리자 연결 관리자 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- SQL13.DTS.DESIGNER.AFPARMCM.F1
- SQL14.DTS.DESIGNER.AFPARMCM.F1
ms.assetid: 8ce8024f-153f-4066-b607-0d36fefc79ed
caps.latest.revision: 3
author: Lingxi-Li
ms.author: lingxl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: dd1dbf668bf3ac24d9d6598b0ff9e2256d897c42
ms.contentlocale: ko-kr
ms.lasthandoff: 09/26/2017

---
# <a name="azure-resource-manager-connection-manager"></a>Azure 리소스 관리자 연결 관리자
**Azure 리소스 관리자 연결 관리자** SSIS 패키지를 사용 하 여 Azure 리소스 관리를 통해는 [서비스 사용자](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-create-service-principal-portal)합니다.

**Azure 리소스 관리자 연결 관리자** 의 구성 요소는 [Azure에 대 한 SQL Server Integration Services (SSIS) 기능 팩](../../integration-services/azure-feature-pack-for-integration-services-ssis.md)합니다.

만들고 구성 하는 **Azure 리소스 관리자 연결 관리자**, 다음 단계를 수행 합니다.

1. 에 **SSIS 연결 관리자 추가** 대화 상자에서 **AzureResourceManager**를 클릭 하 고 **추가**합니다.
2. 에 **Azure 리소스 관리자 연결 관리자 편집기** 대화 상자를 지정 된 **응용 프로그램 ID**, **응용 프로그램 키**, 및 **테 넌 트 ID** 서비스 사용자에 대 한 합니다. 이러한 속성에 대 한 자세한 내용은를 참조 하십시오 [이](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-create-service-principal-portal) 문서.
3. **확인** 을 클릭하여 대화 상자를 닫습니다.
4. 작성한 연결 관리자의 속성은 **속성** 창에서 확인할 수 있습니다.

