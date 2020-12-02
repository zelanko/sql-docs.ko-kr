---
description: Azure Resource Manager 연결 관리자
title: Azure Resource Manager 연결 관리자 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- SQL13.DTS.DESIGNER.AFPARMCM.F1
- SQL14.DTS.DESIGNER.AFPARMCM.F1
ms.assetid: 8ce8024f-153f-4066-b607-0d36fefc79ed
author: Lingxi-Li
ms.author: lingxl
ms.openlocfilehash: 84b9c97935d0bcf89a4741304bb9a1e6b3576605
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/25/2020
ms.locfileid: "96130130"
---
# <a name="azure-resource-manager-connection-manager"></a>Azure Resource Manager 연결 관리자

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


**Azure Resource Manager 연결 관리자** 를 통해 SSIS 패키지는 [서비스 사용자](/azure/azure-resource-manager/resource-group-create-service-principal-portal)를 사용하여 Azure 리소스를 관리할 수 있습니다.

**Azure Resource Manager 연결 관리자** 는 [Azure용 SSIS(SQL Server Integration Services) 기능 팩](../../integration-services/azure-feature-pack-for-integration-services-ssis.md)의 구성 요소입니다.

**Azure Resource Manager 연결 관리자** 를 만들고 구성하려면 다음 단계를 수행합니다.

1. **SSIS 연결 관리자 추가** 대화 상자에서 **AzureResourceManager** 를 선택하고 **추가** 를 클릭합니다.
2. **Azure Resource Manager 연결 관리자 편집기** 대화 상자에서 서비스 사용자에 대한 **애플리케이션 ID**, **애플리케이션 키** 및 **테넌트 ID** 를 지정합니다. 이러한 속성에 대한 자세한 내용은 [이](/azure/azure-resource-manager/resource-group-create-service-principal-portal) 문서를 참조하세요.
3. **확인** 을 클릭하여 대화 상자를 닫습니다.
4. 작성한 연결 관리자의 속성은 **속성** 창에서 확인할 수 있습니다.