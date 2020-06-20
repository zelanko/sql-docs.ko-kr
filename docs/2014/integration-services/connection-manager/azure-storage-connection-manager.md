---
title: Azure Storage 연결 관리자 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.afpstorageconn.f1
- sql11.dts.designer.afpstorageconn.f1
ms.assetid: 68bd1d04-d20f-4357-a34e-7c9c76457062
author: janinezhang
ms.author: janinez
ms.openlocfilehash: c6b6c86aa3f76088ff3cb0e36a1a111b325944ea
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84921094"
---
# <a name="azure-storage-connection-manager"></a>Azure Storage 연결 관리자
  SSIS 패키지는 Azure Storage 연결 관리자를 통해 속성으로 지정된 값(스토리지 계정 이름 및 계정 키)을 사용하여 Azure Storage 계정에 연결할 수 있습니다.  
  
1.  **SSIS 연결 관리자 추가** 대화 상자에서 **AzureStorage**를 선택하고 **추가**를 클릭합니다.  
  
2.  Azure Storage 연결 관리자 편집기 대화 상자에서 **Azure 계정 사용**을 선택하여 인터넷을 통해 Azure Storage 서비스에 연결하거나 **로컬 개발자 계정 사용**을 선택하여 Azure Storage 에뮬레이터가 호스트하는 로컬 서비스에 연결합니다.  
  
3.  **Azure 계정 사용** 옵션을 선택하는 경우 다음 단계를 수행합니다.  
  
    1.  **스토리지 계정 이름** 및 **계정 키** 필드의 값을 지정합니다. 이러한 값은 SSIS 패키지에 중요한 데이터로 저장됩니다.  
  
    2.  HTTP 대신 HTTPS를 사용하여 Azure Storage 서비스에 연결하려면 **HTTPS 사용**을 선택합니다.  
  
4.  **확인** 을 클릭하여 대화 상자를 닫습니다.  
  
5.  작성한 연결 관리자의 속성은 **속성** 창에서 확인할 수 있습니다.  
  
  
