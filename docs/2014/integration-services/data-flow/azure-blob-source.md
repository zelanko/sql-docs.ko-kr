---
title: Azure Blob 원본 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.afpblobsrc.f1
- sql11.dts.designer.afpblobsrc.f1
ms.assetid: 80645c5c-88c8-4fb0-8607-de1bb7bffcbb
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 9feb14f98bec3a1a48526d2c3c72641ad61c48e9
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62828196"
---
# <a name="azure-blob-source"></a>Azure Blob 원본
 SSIS 패키지는 **Azure Blob 원본** 구성 요소를 통해 Azure Blob에서 데이터를 읽을 수 있습니다. 지원되는 파일 형식은 다음과 같습니다. CSV와 AVRO. Azure Blob 원본용 편집기를 표시하려면 데이터 흐름 디자이너에서 **Azure Blob 원본** 을 끌어서 놓고 두 번 클릭하여 편집기를 엽니다.  
  
1.  **Azure 스토리지 연결 관리자** 필드에서는 기존 Azure 스토리지 연결 관리자를 지정하거나 Azure 스토리지 계정을 참조하는 스토리지 연결 관리자를 새로 만듭니다.  
  
2.  **Blob 컨테이너 이름** 필드에서는 원본 파일을 포함하는 Blob 컨테이너의 이름을 지정합니다.  
  
3.  **Blob 이름** 필드에서는 Blob의 경로를 지정합니다.  
  
4.  **Blob 파일 형식** 필드에서는 사용할 Blob 형식을 지정합니다.  
  
5.  파일 형식이 CSV이면 **열 구분 기호 문자** 값을 지정해야 합니다. 파일의 첫 행에 열 이름을 포함하려는 경우에는 **첫 번째 데이터 행의 열 이름** 도 선택합니다.  
  
6.  연결 정보를 지정한 다음 **열** 페이지로 전환하여 SSI 데이터 흐름에 대해 원본 열을 대상 열에 매핑합니다.  
  
  
