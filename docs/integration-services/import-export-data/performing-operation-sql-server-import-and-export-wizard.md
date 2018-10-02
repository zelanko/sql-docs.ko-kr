---
title: 작업 수행(SQL Server 가져오기 및 내보내기 마법사) | Microsoft Docs
ms.custom: ''
ms.date: 01/11/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.impexpwizard.performingoperation.f1
ms.assetid: 83259509-71d6-4a64-a7f2-4e9603b30bd4
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: f1a48018175dd7c0a92a83fdc68d6451324cd2fb
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47738191"
---
# <a name="performing-operation-sql-server-import-and-export-wizard"></a>작업을 수행하는 중(SQL Server 가져오기 및 내보내기 마법사)
마법사에서 선택한 항목을 검토하고 **마법사 완료** 페이지에서 **마침** 클릭하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가져오기 및 내보내기 마법사에 **작업을 수행하는 중**이 표시됩니다. 이 페이지에는 이전 페이지에서 구성한 작업의 진행률 및 결과가 표시됩니다. 이 페이지에서는 어떤 작업도 수행할 필요가 없습니다.

## <a name="screen-shot---operation-in-progress"></a>스크린샷 - 작업 진행 중 
 다음 스크린샷에서는 작업이 계속 진행되는 동안 표시되는 마법사의 **작업을 수행하는 중** 페이지를 보여 줍니다.  
  
 ![가져오기 및 내보내기 마법사의 작업 수행 페이지](../../integration-services/import-export-data/media/performing-operation1.png "가져오기 및 내보내기 마법사의 작업 수행 페이지")  

## <a name="screen-shot---operation-completed"></a>스크린샷 - 작업 완료됨 
 다음 스크린샷에서는 작업이 완료된 후 표시되는 마법사의 **작업을 수행하는 중** 페이지를 보여 줍니다. 해당 단계에 대한 자세한 내용을 보려면 **메시지** 열의 항목을 클릭하세요.  
  
 ![가져오기 및 내보내기 마법사의 작업 수행 페이지](../../integration-services/import-export-data/media/performing-operation2.png "가져오기 및 내보내기 마법사의 작업 수행 페이지")  
  
## <a name="watch-the-progress-of-the-operation"></a>작업 진행률 확인
 **동작**  
 작업의 각 단계를 표시합니다.  
  
 **상태**  
 각 단계의 성공 또는 실패 여부를 표시합니다.  
  
 **메시지**  
 단계에 대한 정보 및 오류 메시지를 표시합니다. 해당 단계에 대한 자세한 내용을 보려면 이 열의 항목을 클릭하세요.

## <a name="interrupt-the-operation-or-save-the-results"></a>작업 중단 또는 결과 저장
 **중지**  
 필요한 경우 **중지** 단추를 클릭하여 작업을 중단합니다.  
  
 **보고서**  
 결과 보고서를 보거나, 보고서를 파일에 저장하거나, 보고서를 클립보드에 복사하거나, 보고서를 전자 메일로 보냅니다.  
  
## <a name="whats-next"></a>다음 단계  
 구성한 작업이 실행되고 완료되면 실행 중인 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가져오기 및 내보내기 마법사를 마친 것입니다.  
-   즉시 작업을 실행한 경우 선택한 대상을 열어 마법사에서 복사한 데이터를 검토할 수 있습니다.  
-   마법사에서 만든 SSIS 패키지를 저장한 경우 SQL Server Data Tools에서 열어 사용자 지정하고 다시 사용할 수 있습니다. 저장된 패키지를 사용자 지정하고 나중에 다시 실행하는 방법에 대한 자세한 내용은 [SSIS 패키지 저장](../../integration-services/import-export-data/save-ssis-package-sql-server-import-and-export-wizard.md)을 참조하세요.

## <a name="see-also"></a>관련 항목:
[가져오기 및 내보내기 마법사의 이 간단한 예제로 시작](../../integration-services/import-export-data/get-started-with-this-simple-example-of-the-import-and-export-wizard.md)


