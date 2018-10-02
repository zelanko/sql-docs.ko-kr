---
title: Azure Blob 원본 | Microsoft Docs
ms.custom: ''
ms.date: 08/20/2018
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.afpblobsrc.f1
- sql14.dts.designer.afpblobsrc.f1
ms.assetid: 80645c5c-88c8-4fb0-8607-de1bb7bffcbb
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 61c4f6794e5d491fa1b7d935e54d470734a99d10
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47698771"
---
# <a name="azure-blob-source"></a>Azure Blob 원본
  SSIS 패키지는 **Azure Blob 원본** 구성 요소를 통해 Azure Blob에서 데이터를 읽을 수 있습니다. 지원되는 파일 형식은 CSV 및 AVRO입니다.
  
  Azure Blob 원본용 편집기를 표시하려면 데이터 흐름 디자이너에서 **Azure Blob 원본** 을 끌어서 놓고 두 번 클릭하여 편집기를 엽니다.  
  
 **Azure Blob 원본**은 [Azure용 SSIS(SQL Server Integration Services) 기능 팩](../../integration-services/azure-feature-pack-for-integration-services-ssis.md)의 구성 요소입니다.  
  
1.  **Azure 저장소 연결 관리자** 필드에서는 기존 Azure 저장소 연결 관리자를 지정하거나 Azure 저장소 계정을 참조하는 저장소 연결 관리자를 새로 만듭니다.  
  
2.  **Blob 컨테이너 이름** 필드에서는 원본 파일을 포함하는 Blob 컨테이너의 이름을 지정합니다.  
  
3.  **Blob 이름** 필드에서는 Blob의 경로를 지정합니다.  
  
4.  **Blob 파일 형식** 필드에서는 사용할 Blob 형식을 **Text** 또는 **Avro**로 지정합니다.  
  
5.  파일 형식이 **Text**이면 **열 구분 기호 문자** 값을 지정해야 합니다. (다문자 구분 기호는 지원되지 않습니다.)

    파일의 첫 행에 열 이름을 포함하려는 경우에는 **첫 번째 데이터 행의 열 이름** 도 선택합니다.

6.  파일이 압축된 경우 **파일 압축 풀기**를 선택합니다.

7.  파일이 압축된 경우 **압축 유형**으로 **GZIP**, **DEFLATE** 또는 **BZIP2**를 선택합니다. Zip 형식은 지원되지 않습니다.
  
8.  연결 정보를 지정한 후 **열** 페이지로 전환하여 SSIS 데이터 흐름의 원본 열을 대상 열에 매핑합니다.  
  
  
