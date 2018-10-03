---
title: Azure Storage 연결 관리자 | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.afpstorageconn.f1
- sql14.dts.designer.afpstorageconn.f1
ms.assetid: 68bd1d04-d20f-4357-a34e-7c9c76457062
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 31440d6479353467d687467466f9c838a49d5252
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47724151"
---
# <a name="azure-storage-connection-manager"></a>Azure 저장소 연결 관리자
  SSIS 패키지는 **Azure 저장소 연결 관리자** 를 통해 속성으로 지정된 값(저장소 계정 이름 및 계정 키)을 사용하여 Azure 저장소 계정에 연결할 수 있습니다.  
   
 **Azure Storage 연결 관리자**는 [Azure용 SSIS(SQL Server Integration Services) 기능 팩](../../integration-services/azure-feature-pack-for-integration-services-ssis.md)의 구성 요소입니다. 
  
1.  **SSIS 연결 관리자 추가** 대화 상자에서 **AzureStorage**를 선택하고 **추가**를 클릭합니다.  
  
2.  Azure 저장소 연결 관리자 편집기 대화 상자에서 **Azure 계정 사용** 을 선택하여 인터넷을 통해 Azure 저장소 서비스에 연결하거나 **로컬 개발자 계정 사용** 을 선택하여 Azure 저장소 에뮬레이터가 호스트하는 로컬 서비스에 연결합니다.  
  
3.  **Azure 계정 사용** 옵션을 선택하는 경우 다음 단계를 수행합니다.  
  
    1.  **저장소 계정 이름** 및 **계정 키** 필드의 값을 지정합니다. 이러한 값은 SSIS 패키지에 중요한 데이터로 저장됩니다.  
  
    2.  HTTP 대신 HTTPS를 사용하여 Azure 저장소 서비스에 연결하려면 **HTTPS 사용** 을 선택합니다.  
  
4.  **확인** 을 클릭하여 대화 상자를 닫습니다.  
  
5.  작성한 연결 관리자의 속성은 **속성** 창에서 확인할 수 있습니다.  
  
  
