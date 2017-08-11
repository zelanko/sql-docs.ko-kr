---
title: "데이터 처리 확장 프로그램 구현 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- custom data processing extensions [Reporting Services]
- data sources [Reporting Services], data processing extensions
- data processing extensions [Reporting Services]
- extensions [Reporting Services], data processing
ms.assetid: 8dc2b44e-5ad9-411d-a29f-7213e29321a9
caps.latest.revision: 35
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: a6aab5e722e732096e9e4ffdf458ac25088e09ae
ms.openlocfilehash: 1497690ebccc010601542308747240d0e91d89db
ms.contentlocale: ko-kr
ms.lasthandoff: 08/03/2017

---
# <a name="implementing-a-data-processing-extension"></a>데이터 처리 확장 프로그램 구현
  [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]의 데이터 처리 확장 프로그램을 통해 데이터 원본에 연결하고 데이터를 검색할 수 있습니다. 이 프로그램은 데이터 원본과 데이터 집합을 연결하는 역할도 합니다. [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]데이터 처리 확장 프로그램의 하위 집합을 본떠서는 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 데이터 공급자 인터페이스입니다.  
  
## <a name="in-this-section"></a>섹션 내용  
 [데이터 처리 확장 프로그램 개요](../../../reporting-services/extensions/data-processing/data-processing-extensions-overview.md)  
 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]용 사용자 지정 데이터 처리 확장 프로그램을 작성하는 방법을 소개합니다.  
  
 [데이터 처리 확장 프로그램 구현 준비](../../../reporting-services/extensions/data-processing/preparing-to-implement-a-data-processing-extension.md)  
 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 데이터 처리 확장 프로그램을 구현할 때 및 특정 인터페이스를 구현해야 할 때 사용할 수 있는 인터페이스에 대해 설명합니다.  
  
 [데이터 처리 확장 프로그램 라이브러리 만들기](../../../reporting-services/extensions/data-processing/creating-a-data-processing-extension-library.md)  
 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 데이터 처리 확장 프로그램에 대한 네임스페이스 할당에 대해 설명하고 데이터 처리 확장 프로그램을 라이브러리 DLL로 컴파일하는 방법에 대해 설명합니다.  
  
 [데이터 처리 확장 프로그램에 대 한 Connection 클래스 구현](../../../reporting-services/extensions/data-processing/implementing-a-connection-class-for-a-data-processing-extension.md)  
 한 연결 및 자체적으로 구현 하는 방법의 속성을 설명 **연결** 데이터 처리 확장 프로그램에 대 한 클래스입니다.  
  
 [데이터 처리 확장 프로그램에 대 한 Command 클래스 구현](../../../reporting-services/extensions/data-processing/implementing-a-command-class-for-a-data-processing-extension.md)  
 명령 및 자체적으로 구현 하는 방법의 속성을 설명 **명령** 데이터 처리 확장 프로그램에 대 한 클래스입니다.  
  
 [데이터 처리 확장 프로그램에 대 한 DataReader 클래스 구현](../../../reporting-services/extensions/data-processing/implementing-a-datareader-class-for-a-data-processing-extension.md)  
 자체적으로 구현 하는 방법과 데이터 판독기의 특성을 설명 **DataReader** 데이터 처리 확장 프로그램에 대 한 클래스입니다.  
  
 [외부 데이터 집합을 사용 하 여 Reporting services](../../../reporting-services/extensions/data-processing/using-an-external-dataset-with-reporting-services.md)  
 사용자 지정을 노출 하는 방법에 설명 **DataSet** 소비에 대 한 보고서 서버에는 개체입니다.  
  
 [데이터 처리 확장 프로그램 배포](../../../reporting-services/extensions/data-processing/deploying-a-data-processing-extension.md)  
 데이터 처리 확장 프로그램을 배포하는 방법을 설명합니다.  
  
 [데이터 처리 확장 프로그램 코드 디버깅](../../../reporting-services/extensions/data-processing/debugging-data-processing-extension-code.md)  
 데이터 처리 확장 프로그램에서 코드를 디버깅하는 방법을 설명합니다.  
  
 [데이터 처리 확장 프로그램 제거](../../../reporting-services/extensions/data-processing/removing-a-data-processing-extension.md)  
 보고서 서버 또는 보고서 디자이너에서 데이터 처리 확장 프로그램을 제거하는 방법을 설명합니다.  
  
 완전히 구현 된 데이터 처리 확장 프로그램의 샘플을 보려면 [SQL Server Reporting Services 제품 샘플](http://go.microsoft.com/fwlink/?LinkId=177889)합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [Reporting Services 확장 프로그램](../../../reporting-services/extensions/reporting-services-extensions.md)   
 [Reporting Services 확장 프로그램 라이브러리](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  
