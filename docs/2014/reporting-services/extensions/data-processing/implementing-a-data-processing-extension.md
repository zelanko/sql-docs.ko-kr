---
title: 데이터 처리 확장 프로그램 구현 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.topic: reference
helpviewer_keywords:
- custom data processing extensions [Reporting Services]
- data sources [Reporting Services], data processing extensions
- data processing extensions [Reporting Services]
- extensions [Reporting Services], data processing
ms.assetid: 8dc2b44e-5ad9-411d-a29f-7213e29321a9
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 4ca26d9b4af7adebda9f5bf0021ba7871f8425aa
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/13/2018
ms.locfileid: "53358297"
---
# <a name="implementing-a-data-processing-extension"></a>데이터 처리 확장 프로그램 구현
  [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]의 데이터 처리 확장 프로그램을 통해 데이터 원본에 연결하고 데이터를 검색할 수 있습니다. 이 프로그램은 데이터 원본과 데이터 집합을 연결하는 역할도 합니다. [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 데이터 처리 확장 프로그램은 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 데이터 공급자 인터페이스의 하위 집합을 본떠서 만든 것입니다.  
  
## <a name="in-this-section"></a>섹션 내용  
 [데이터 처리 확장 프로그램 개요](data-processing-extensions-overview.md)  
 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]용 사용자 지정 데이터 처리 확장 프로그램을 작성하는 방법을 소개합니다.  
  
 [데이터 처리 확장 프로그램 구현 준비](preparing-to-implement-a-data-processing-extension.md)  
 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 데이터 처리 확장 프로그램을 구현할 때 및 특정 인터페이스를 구현해야 할 때 사용할 수 있는 인터페이스에 대해 설명합니다.  
  
 [데이터 처리 확장 라이브러리 만들기](creating-a-data-processing-extension-library.md)  
 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 데이터 처리 확장 프로그램에 대한 네임스페이스 할당에 대해 설명하고 데이터 처리 확장 프로그램을 라이브러리 DLL로 컴파일하는 방법에 대해 설명합니다.  
  
 [데이터 처리 확장 프로그램에 대한 Connection 클래스 구현](implementing-a-connection-class-for-a-data-processing-extension.md)  
 연결의 특성 및 데이터 처리 확장 프로그램에 대해 고유의 **Connection** 클래스를 구현하는 방법을 설명합니다.  
  
 [데이터 처리 확장 프로그램에 대한 Command 클래스 구현](implementing-a-command-class-for-a-data-processing-extension.md)  
 명령의 특성 및 데이터 처리 확장 프로그램에 대해 고유의 **Command** 클래스를 구현하는 방법을 설명합니다.  
  
 [데이터 처리 확장 프로그램에 대한 DataReader 클래스 구현](implementing-a-datareader-class-for-a-data-processing-extension.md)  
 데이터 판독기의 특성 및 데이터 처리 확장 프로그램에 대해 고유의 **DataReader** 클래스를 구현하는 방법을 설명합니다.  
  
 [Reporting Services에서 외부 데이터 세트 사용](using-an-external-dataset-with-reporting-services.md)  
 사용자 지정 **DataSet** 개체를 보고서 서버에서 사용할 수 있도록 표시하는 방법을 설명합니다.  
  
 [데이터 처리 확장 프로그램 배포](deploying-a-data-processing-extension.md)  
 데이터 처리 확장 프로그램을 배포하는 방법을 설명합니다.  
  
 [데이터 처리 확장 프로그램 코드 디버깅](debugging-data-processing-extension-code.md)  
 데이터 처리 확장 프로그램에서 코드를 디버깅하는 방법을 설명합니다.  
  
 [데이터 처리 확장 프로그램 제거](removing-a-data-processing-extension.md)  
 보고서 서버 또는 보고서 디자이너에서 데이터 처리 확장 프로그램을 제거하는 방법을 설명합니다.  
  
 완전히 구현된 데이터 처리 확장 프로그램 예는 [SQL Server Reporting Services 제품 예제](https://go.microsoft.com/fwlink/?LinkId=177889)를 참조하십시오.  
  
## <a name="see-also"></a>관련 항목:  
 [Reporting Services 확장 프로그램](../reporting-services-extensions.md)   
 [Reporting Services 확장 라이브러리](../reporting-services-extension-library.md)  
  
  
