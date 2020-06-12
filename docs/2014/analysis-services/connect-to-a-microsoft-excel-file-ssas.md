---
title: Microsoft Excel 파일에 연결 (SSAS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.bidtoolset.connexcelfile.f1
ms.assetid: 126f7d6b-d270-40e7-b23e-8d114f87065b
author: minewiskan
ms.author: owend
ms.openlocfilehash: 6646ee55ce6703391b5c146d41d513445aa2fabd
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/08/2020
ms.locfileid: "84527189"
---
# <a name="connect-to-a-microsoft-excel-file-ssas"></a>Microsoft Excel 파일에 연결(SSAS)
  **테이블 가져오기 마법사** 의 이 페이지에서는 로컬 컴퓨터에 저장되어 있는 Microsoft Excel 파일에 연결할 수 있습니다. [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]에서 마법사에 액세스하려면 **모델** 메뉴에서 **데이터 원본에서 가져오기**를 클릭합니다.  
  
 Microsoft Excel 파일에 연결하려면 컴퓨터에 적절한 ACE 공급자를 설치해야 합니다. 자세한 내용은 [지원되는 데이터 원본&#40;SSAS 테이블 형식&#41;](tabular-models/data-sources-supported-ssas-tabular.md)을 참조하세요.  
  
> [!NOTE]  
>  이 페이지에서 파일을 선택하는 경우 현재 사용자의 자격 증명이 사용됩니다. 하지만 가장 정보 페이지에 지정된 사용자에게 선택한 파일을 읽을 수 있는 권한이 없는 경우에는 가져오기 작업이 실패합니다.  
  
## <a name="ui-element-list"></a>UI 요소 목록  
 **연결 이름**  
 이 데이터 원본 연결의 고유 이름을 입력합니다. 이 이름은 반드시 입력해야 합니다.  
  
 **Excel 파일 경로**  
 Excel 파일의 전체 경로를 지정합니다.  
  
 **찾아보기**  
 Excel 파일을 사용할 수 있는 위치로 이동합니다.  
  
 **고급**  
 **고급 속성 설정** 대화 상자를 사용 하 여 추가 연결 속성을 설정 합니다.  
  
 **첫 행을 열 머리글로 사용**  
 첫 번째 데이터 행을 대상 테이블의 열 머리글로 사용할지 여부를 지정합니다.  
  
 **연결을 테스트**  
 현재 설정을 사용하여 데이터 원본에 대한 연결을 설정해 봅니다. 연결이 성공적인지 여부를 나타내는 메시지가 표시됩니다.  
  
  
