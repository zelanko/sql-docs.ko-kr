---
title: CRI 변환 대화 상자(보고서 작성기) | Microsoft Docs
description: 보고서 작성기에서는 지원되지 않는 기능을 갖는 일부 사용자 지정 보고서 항목을 새로운 보고서 정의 형식으로 변환하라는 메시지를 표시합니다.
ms.date: 08/17/2018
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-builder
ms.topic: reference
f1_keywords:
- "10008"
helpviewer_keywords:
- CRI
- custom report items
ms.assetid: 2a3f2ac6-667e-4498-8b73-9c40beb993f5
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 5c3d7ece0e4bccf6bea6426391498005887ef6c8
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2020
ms.locfileid: "80342901"
---
# <a name="convert-cri-dialog-box-report-builder"></a>CRI 변환 대화 상자(보고서 작성기)

  이 보고서에는 지원되지 않는 기능이 있는 CRI(사용자 지정 보고서 항목)가 포함되어 있습니다. CRI는 보고서에 데이터를 표시하는 사용자 지정 개체를 지원하는 RDL(Report Definition Language)에 대한 확장입니다. CRI에는 타사 소프트웨어 공급업체에서 제공하는 디자인 타임 및 런타임 구성 요소가 포함되어 있습니다.  
  
> [!NOTE]  
>  보고서 서버에서 사용자 지정 항목을 지원하도록 선택하는 것은 시스템 관리자가 결정할 일입니다. 보고서에서 CRI를 보려는 경우 보고서를 미리 보려면 보고서 제작 클라이언트에 CRI 구성 요소를 설치해야 하고 게시 또는 업로드된 보고서를 보려면 보고서 서버에 CRI 구성 요소를 설치해야 합니다.  
  
 일부 CRI를 새 보고서 정의 형식의 보고서 항목으로 변환할 수 있습니다. 보고서를 열면 업그레이드할 것인지 묻는 메시지가 나타납니다. 다음 정보를 사용하여 이 보고서에서 CRI를 변환할지 여부를 결정할 수 있습니다.  
  
-   **예** 가능한 경우 보고서의 모든 CRI를 변환하려면 **예** 를 선택합니다. CRI에서 지원하지 않는 기능은 업그레이드할 수 없으며 보고서 정의 파일에서 제거됩니다. 지원하지 않는 기능 목록은 [보고서 업그레이드](../../reporting-services/install-windows/upgrade-reports.md)를 참조하세요. 보고서를 볼 때 CRI가 보고서에 다른 방식으로 표시될 수 있습니다.  
  
-   **아니요** 보고서에서 CRI를 변환하지 않으려면 **아니요** 를 선택합니다. 이러한 CRI는 현재 버전의 보고서 처리기에서는 표시할 수 없습니다. 시스템 관리자가 새 보고서 정의 형식과 호환되는 타사 소프트웨어 공급업체가 제공하는 새 버전의 CRI를 설치하려는 경우에는 **아니요**를 선택해야 합니다. 새 버전을 사용할 수 있을 때까지 보고서에 CRI가 빨간색 X가 있는 비어 있는 입력란으로 표시됩니다.  
  
 두 경우 모두 보고서는 새 보고서 정의 형식으로 업그레이드되며 원래 보고서의 백업 복사본은 *\<보고서 이름>* `-` Backup.rdl로 저장됩니다. 보고서를 보고서 작성 도구에 저장하는 경우 업그레이드된 보고서가 새 보고서 정의 형식으로 저장됩니다. 보고서를 게시하는 경우 보고서는 컴퓨터에 먼저 저장된 다음 보고서 서버에 게시됩니다. 업그레이드된 버전의 보고서가 보고서 서버에 게시됩니다.  
  
 보고서를 저장하지 않는 경우 원래 보고서가 그대로 유지됩니다. 그러나 이 보고서를 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 의 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 이상 버전 또는 이 보고서 정의 형식을 사용하는 보고서 제작 환경에서 편집할 수는 없습니다. 보고서 관리자를 사용하여 보고서를 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상의 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 보고서 서버로 업로드하면 원래 버전의 보고서를 계속 실행할 수 있습니다. 자세한 내용은 [파일 또는 보고서 업로드&#40;보고서 관리자&#41;](../../reporting-services/reports/upload-a-file-or-report-report-manager.md)를 참조하세요.  
  
 보고서 서버에 게시하는 대신 보고서를 업로드하는 경우 보고서 처리기가 처음 사용 시 보고서 업그레이드 가능 여부를 결정합니다. 업그레이드가 불가능한 보고서는 이전 버전과의 호환성 모드에서 처리되며 계속해서 이전 버전의 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]로 표시됩니다. 자세한 내용은 [Upgrade Reports](../../reporting-services/install-windows/upgrade-reports.md)을(를) 참조하세요.  
  
 보고서, 보고서 서버 또는 보고서 작성 환경에 대한 현재 보고서 정의 형식을 식별하려면 [보고서 정의 스키마 버전 찾기&#40;SSRS&#41;](../../reporting-services/reports/find-the-report-definition-schema-version-ssrs.md)를 참조하세요.  

  
  
