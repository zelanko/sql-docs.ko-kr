---
title: Azure Resource Manager 연결 관리자 | Microsoft Docs
ms.custom: ''
ms.date: 02/28/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- SQL12.DTS.DESIGNER.AFPARMCM.F1
- SQL11.DTS.DESIGNER.AFPARMCM.F1
ms.assetid: a2380258-0418-4a8c-a731-5071a44ddf1e
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: a275b540d6199183475298e6a32940ba272f9bc3
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48072453"
---
# <a name="azure-resource-manager-connection-manager"></a>Azure Resource Manager 연결 관리자
**Azure Resource Manager 연결 관리자**를 통해 SSIS 패키지는 [서비스 사용자](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-create-service-principal-portal)를 사용하여 Azure 리소스를 관리할 수 있습니다.

**Azure Resource Manager 연결 관리자**를 만들고 구성하려면 다음 단계를 수행합니다.

1. **SSIS 연결 관리자 추가** 대화 상자에서 **AzureResourceManager**를 선택하고 **추가**를 클릭합니다.
2. **Azure Resource Manager 연결 관리자 편집기** 대화 상자에서 서비스 사용자에 대한 **응용 프로그램 ID**, **응용 프로그램 키** 및 **테넌트 ID**를 지정합니다. 이러한 속성에 대한 자세한 내용은 [이](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-create-service-principal-portal) 문서를 참조하세요.
3. **확인** 을 클릭하여 대화 상자를 닫습니다.
4. 작성한 연결 관리자의 속성은 **속성** 창에서 확인할 수 있습니다.
