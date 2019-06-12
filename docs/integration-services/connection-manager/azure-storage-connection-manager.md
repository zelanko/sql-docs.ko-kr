---
title: Azure Storage 연결 관리자 | Microsoft Docs
ms.custom: ''
ms.date: 05/22/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.afpstorageconn.f1
- sql14.dts.designer.afpstorageconn.f1
ms.assetid: 68bd1d04-d20f-4357-a34e-7c9c76457062
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 03acf5db82c21a66e2fbd8337713b6989ce36a31
ms.sourcegitcommit: fc0eb955b41c9c508a1fe550eb5421c05fbf11b4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/30/2019
ms.locfileid: "66403066"
---
# <a name="azure-storage-connection-manager"></a>Azure Storage 연결 관리자

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]

  **Azure Storage 연결 관리자**를 사용하여 SSIS 패키지가 Azure Storage 계정에 연결할 수 있습니다.
   
 **Azure Storage 연결 관리자**는 [Azure용 SSIS(SQL Server Integration Services) 기능 팩](../../integration-services/azure-feature-pack-for-integration-services-ssis.md)의 구성 요소입니다. 
  
**SSIS 연결 관리자 추가** 대화 상자에서 **AzureStorage**를 선택하고 **추가**를 클릭합니다.  
  
사용할 수 있는 속성은 다음과 같습니다.

- **서비스:** 연결할 스토리지 서비스를 지정합니다.
- **계정 이름**: 스토리지 계정 이름을 지정합니다.
- **인증:** 사용할 인증 방법을 지정합니다. **AccessKey** 및 **ServicePrincipal** 인증이 지원됩니다.
    - **AccessKey:** 이 인증 방법에 대해 **계정 키**를 지정합니다.
    - **ServicePrincipal:** 이 인증 방법에 대해 서비스 주체의 **애플리케이션 ID**, **애플리케이션 키**, **테넌트 ID**를 지정합니다.
      서비스 주체에는 스토리지 계정의 **Storage Blob 데이터 기여자** 역할을 할당해야 합니다.
      세부 정보는 [이](https://docs.microsoft.com/azure/storage/common/storage-auth-aad-rbac-portal#assign-rbac-roles-using-the-azure-portal) 페이지를 참조하세요.
- **환경:** 스토리지 계정을 호스팅하는 클라우드 환경을 지정합니다.
