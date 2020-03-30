---
title: 변환 검사를 수행하지 않고 형식 변환(SQL Server 가져오기-내보내기 마법사) | Microsoft Docs
ms.custom: ''
ms.date: 01/11/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.impexpwizard.nomappingfile.f1
ms.assetid: 87d9d3e5-477f-4117-a37f-bff53ea3e14d
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 8a6f07634f9f4a3fba48889391a4bfc9e4e245df
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2020
ms.locfileid: "71285322"
---
# <a name="convert-types-without-conversion-checking-sql-server-import-and-export-wizard"></a>변환 검사를 수행하지 않고 형식 변환(SQL Server 가져오기 및 내보내기 마법사)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  복사할 기존 테이블 및 뷰를 선택하거나 제공한 쿼리를 검토한 후에는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가져오기 및 내보내기 마법사에 **변환 검사를 수행하지 않고 형식 변환**이 표시될 수 있습니다. 마법사에서는 원본과 대상 간에 데이터 형식을 매핑하는 데 필요한 하나 이상의 데이터 형식 변환 및 매핑 파일을 찾을 수 없는 경우 이 페이지를 표시합니다. 이 페이지에는 누락된 항목을 파악하는 데 도움이 되는 정보가 포함됩니다.
  
 데이터 형식 변환의 성공 여부를 확인하지 않고 계속하려면 **다음** 을 클릭합니다. 그러지 않으면 **뒤로** 를 클릭하여 선택 항목을 변경하거나 **취소** 를 클릭하여 마법사를 종료합니다.

## <a name="screen-shot-of-the-convert-types-page"></a>형식 변환 페이지의 스크린샷  
  
다음 스크린샷에서는 마법사의 **변환 검사를 수행하지 않고 형식 변환** 페이지 예를 보여 줍니다.

![형식 변환](../../integration-services/import-export-data/media/convert-types.png)

여기서 문제는 마법사가 선택한 대상에 대한 데이터 형식을 매핑하는 매핑 파일을 찾을 수 없는 것입니다.

이 페이지의 정보에는 누락된 매핑 파일의 이름이 포함되지 않습니다. 마법사에서 지정된 데이터 공급자에 대한 파일이 있는지 여부를 모르므로 누락된 파일의 이름을 제공할 수 없습니다.

## <a name="whats-next"></a>다음 단계  
 **다음** 을 클릭하여 데이터 형식 변환의 성공 여부를 확인하지 않고 계속할 경우 다음 페이지는 **패키지 저장 및 실행**입니다. 이 페이지에서는 복사 작업을 즉시 실행할지 여부를 지정합니다. 구성에 따라 마법사에서 만든 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지를 저장하여 사용자 지정하고 나중에 다시 사용할 수도 있습니다. 자세한 내용은 [패키지 저장 및 실행](../../integration-services/import-export-data/save-and-run-package-sql-server-import-and-export-wizard.md)을 참조하세요.  

## <a name="see-also"></a>참고 항목
[SQL Server 가져오기 및 내보내기 마법사에서 데이터 형식 매핑](../../integration-services/import-export-data/data-type-mapping-in-the-sql-server-import-and-export-wizard.md)
