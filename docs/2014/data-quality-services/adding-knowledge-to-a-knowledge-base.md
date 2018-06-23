---
title: 기술 자료에 정보 추가 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- data-quality-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: da148a7f-55bc-4990-a157-e61968b831d7
caps.latest.revision: 13
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: ebc2c0abd5f380dd31201908e81ac88bfead1232
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36182328"
---
# <a name="adding-knowledge-to-a-knowledge-base"></a>기술 자료에 정보 추가
  이 항목에서는 DQS( [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] )의 기술 자료에 정보를 추가할 수 있는 방법에 대해 설명합니다. 데이터 품질 작업을 수행하려면 먼저 데이터에 대한 정보가 있어야 합니다. 데이터 품질 기술 자료를 만들고 유지 관리하며 여기에 특정 유형의 데이터 원본과 관련된 정보를 추가하는 방식으로 이러한 정보를 얻을 수 있습니다. 기술 자료는 데이터 관련 지식의 리포지토리로서 데이터를 이해하고 데이터의 무결성을 유지하는 데 사용됩니다.  
  
 기술 자료에는 데이터 원본과 관련된 데이터 도메인이 포함되어 있습니다. 각 데이터 도메인에 대해 DQKB는 식별된 모든 용어, 맞춤법 검사 오류, 유효성 검사 및 비즈니스 규칙, 데이터 원본에 대한 데이터 품질 작업을 수행하는 데 사용할 수 있는 참조 데이터 등을 저장합니다. DQS에서는 이 정보를 사용하여 잘못되거나 유효하지 않은 데이터를 식별하고 일치를 수행합니다.  
  
 다음과 같은 컴퓨터 기반 또는 대화형 방식으로 기술 자료에 정보를 추가할 수 있습니다.  
  
-   [기술 자료 검색 수행](#Discovery)  
  
-   [도메인의 데이터 값 관리](#ManageDomain)  
  
-   [.dqs 파일에서 정보 가져오기](#DQSFile)  
  
-   [Excel 파일에서 정보 가져오기](#Excel)  
  
-   [프로젝트에서 다시 기술 자료로 정보 가져오기](#Project)  
  
-   [기본 DQS 기술 자료 사용](#Default)  
  
##  <a name="Discovery"></a> 기술 자료 검색 수행  
 기술 자료 검색에서는 데이터 샘플이 데이터 품질 기준에 맞는지 분석한 다음 이를 통해 얻은 정보를 기술 자료에 추가합니다. 이는 데이터 불일치 및 구문 오류를 식별하고 데이터에 대한 변경 내용을 제안하는 컴퓨터 기반 프로세스입니다. 기술 자료 검색 작업은 대화형으로 도메인 값을 관리할 수 있는 페이지가 포함된 마법사입니다.  
  
-   자세한 내용은 설명서를 참조 하십시오. [Perform Knowledge Discovery](../../2014/data-quality-services/perform-knowledge-discovery.md)합니다.  
  
-   기술 자료 검색을 수행하는 방법에 대한 데모 비디오를 보려면 [여기](http://msdn.microsoft.com/sqlserver/hh323825.aspx)를 클릭하십시오.  
  
##  <a name="ManageDomain"></a> 도메인의 데이터 값 관리  
 DQS에서는 컴퓨터 기반 기술 자료 검색 작업으로 생성된 메타데이터를 대화형으로 변경 및 보강할 수 있습니다. 이 작업은 도메인 관리 작업에서 수행할 수 있으며, 특정 데이터 값에 변경 내용을 적용할 수 있습니다.  
  
-   자세한 내용은 설명서를 참조 하십시오. [Change Domain Values](../../2014/data-quality-services/change-domain-values.md)합니다.  
  
-   도메인 관리를 수행하는 방법에 대한 데모 비디오를 보려면 [여기](http://msdn.microsoft.com/sqlserver/hh323825.aspx)를 클릭하십시오. 이 비디오에서는 기술 자료 검색 마법사의 도메인 값 관리 페이지에서 도메인 값을 변경합니다. 또한 도메인 관리 작업의 도메인 값 페이지에서 이러한 단계를 수행할 수도 있습니다.  
  
##  <a name="DQSFile"></a> .dqs 파일에서 정보 가져오기  
 .dqs 데이터 파일에서 기존 기술 자료로 도메인을 가져오거나 .dqs에서 새 기술 자료로 전체 기술 자료를 가져올 수 있습니다. 이렇게 하려면 먼저 기존 도메인 또는 기술 자료를 .dqs 파일로 내보내야 합니다. 도메인이 포함된 .dqs 파일은 모든 도메인 파일을 포함하고, 기술 자료가 포함된 .dqs 파일은 도메인 및 일치 정책을 비롯하여 모든 기술 자료 정보를 포함합니다.  
  
-   설명서에서 자세한 내용은 [.dqs 파일에서 도메인 가져오기](../../2014/data-quality-services/import-a-domain-from-a-dqs-file.md) 또는 [.dqs 파일에서 기술 자료 가져오기](../../2014/data-quality-services/import-a-knowledge-base-from-a-dqs-file.md)를 참조하세요.  
  
##  <a name="Excel"></a> Excel 파일에서 정보 가져오기  
 Excel 스프레드시트 파일에서 기존 도메인 또는 기술 자료로 도메인 값을 가져올 수 있습니다. 이렇게 하려면 먼저 가져올 도메인 값이 있는 Excel 스프레드시트를 만들고 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] 를 사용하여 값을 가져올 수 있도록 [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]컴퓨터에 Excel이 설치되어 있는지 확인해야 합니다. 도메인 또는 기술 자료에서 Excel 파일로 도메인 값을 내보낼 수는 없습니다.  
  
-   설명서에서 자세한 내용은 [Excel 파일에서 도메인으로 값 가져오기](../../2014/data-quality-services/import-values-from-an-excel-file-into-a-domain.md) 또는 [기술 자료 검색 시 Excel 파일에서 도메인 가져오기](../../2014/data-quality-services/import-domains-from-an-excel-file-in-knowledge-discovery.md)를 참조하세요.  
  
##  <a name="Project"></a> 프로젝트에서 다시 기술 자료로 정보 가져오기  
 기술 자료를 사용하여 정리 또는 일치 데이터 품질 프로젝트를 실행한 후 정리 또는 일치 중에 만든 정보를 해당 기술 자료로 다시 가져올 수 있습니다. 이를 통해 프로젝트 중에 생성된 정보를 유지하고 기술 자료에서 지속적으로 정보를 구축할 수 있습니다.  
  
-   설명서에서 자세한 내용은 [도메인으로 정리 프로젝트 값 가져오기](../../2014/data-quality-services/import-cleansing-project-values-into-a-domain.md)를 참조하세요.  
  
##  <a name="Default"></a> 기본 DQS 기술 자료 사용  
 DQS에서는 미국 회사 및 주소 데이터에 대한 도메인이 포함된 DQS 데이터라는 미리 구축된 기술 자료를 제공합니다. 이 기술 자료를 사용하면 기술 자료를 새로 만들 필요 없이 빠르게 프로젝트를 시작할 수 있습니다. DQS 데이터 기술 자료는 읽기 전용이지만 데이터 관리자가 이를 기반으로 새로운 기술 자료를 만들 수 있습니다.  
  
-   자세한 내용은 설명서를 참조 하십시오. [DQS 기본 기술 자료를 사용 하 여](../../2014/data-quality-services/using-the-dqs-default-knowledge-base.md)합니다.  
  
  