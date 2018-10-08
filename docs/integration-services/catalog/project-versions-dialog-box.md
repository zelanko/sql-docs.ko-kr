---
title: 프로젝트 버전 대화 상자 | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.ssis.ssms.isprojectprop.versions.f1
ms.assetid: a48a387c-2e70-45bc-be2e-26e57a9bb2c4
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 30ab66c12e38aeb6bb1ec355583570d4cbb52c8c
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47840391"
---
# <a name="project-versions-dialog-box"></a>프로젝트 버전 대화 상자
  **프로젝트 버전** 대화 상자를 사용하여 프로젝트 버전을 확인하고 이전 버전으로 복원할 수 있습니다.  
  
 [catalog.object_versions&#40;SSISDB 데이터베이스&#41;](../../integration-services/system-views/catalog-object-versions-ssisdb-database.md) 뷰에서 이전 버전을 보고 [catalog.restore_project&#40;SSISDB Database&#41;](../../integration-services/system-stored-procedures/catalog-restore-project-ssisdb-database.md) 저장 프로시저를 사용하여 이전 버전을 복원할 수도 있습니다.  
  
 **수행 작업**  
  
-   [프로젝트 버전 대화 상자 열기](#open_dialog)  
  
-   [프로젝트 버전 복원](#restore)  
  
##  <a name="open_dialog"></a> 프로젝트 버전 대화 상자 열기  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 서버에 연결합니다.  
  
     즉, [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 데이터베이스를 호스팅하는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 인스턴스에 연결합니다.  
  
2.  개체 탐색기에서 트리를 확장하여 **Integration Services 카탈로그** 노드를 표시합니다.  
  
3.  **Integration Services 카탈로그** 노드를 확장하여 **SSISDB** 노드를 표시합니다.  
  
4.  **SSISDB** 노드는 각각 하나 이상의 프로젝트를 포함하는 하나 이상의 폴더를 포함합니다. 원하는 프로젝트가 포함된 폴더를 확장합니다.  
  
5.  프로젝트를 마우스 오른쪽 단추로 클릭한 다음 **버전**을 클릭합니다.  
  
 **프로젝트 버전** 대화 상자에서 **버전** 테이블에는 서버에 배포된 프로젝트의 버전 목록이 표시되고, 해당 버전이 배포된 날짜 및 시간, 버전이 복원된 날짜 및 시간(복원된 경우), 버전 설명 및 버전 식별자가 함께 표시됩니다. 현재 활성 버전은 테이블의 **현재** 열에 확인 표시가 되어 있습니다.  
  
##  <a name="restore"></a> 프로젝트 버전 복원  
 프로젝트의 이전 버전을 복원하려면 **버전** 테이블에서 버전을 선택하고 **선택한 버전으로 복원**을 클릭합니다. 프로젝트가 선택한 버전으로 복원되고 해당 버전은 **버전** 테이블의 **현재** 열에 확인 표시가 표시됩니다.  
  
  
