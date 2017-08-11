---
title: "데이터 처리 확장 프로그램에 대 한 DataReader 클래스 구현 | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
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
- data processing extensions [Reporting Services], data readers
- data readers [Reporting Services]
- DataReader class
- read-only data
ms.assetid: 23e286e7-6074-4fbe-be29-203420d6c3d0
caps.latest.revision: 35
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: a6aab5e722e732096e9e4ffdf458ac25088e09ae
ms.openlocfilehash: cfd3a6cb38c59b1810d046839cb3be4f0dc9846a
ms.contentlocale: ko-kr
ms.lasthandoff: 08/03/2017

---
# <a name="implementing-a-datareader-class-for-a-data-processing-extension"></a>데이터 처리 확장 프로그램에 대한 DataReader 클래스 구현
  **DataReader** 개체는 클라이언트가 데이터 원본에서 데이터의 읽기 전용, 정방향 전용 스트림을 검색 하는 데 사용 합니다. 쿼리를 실행 하 고 요청할 때까지 클라이언트의 네트워크 버퍼에 저장 된 결과 반환 합니다. 사용 하 여는 **읽기** 의 메서드는 **DataReader** 클래스. 만들려는 **DataReader** 클래스를 구현 <xref:Microsoft.ReportingServices.DataProcessing.IDataReader> 하 고 필요에 따라 구현 <xref:Microsoft.ReportingServices.DataProcessing.IDataReaderExtension>합니다. 사용 하는 **DataReader** 개체 증가 응용 프로그램 성능이 때 즉시 데이터를 검색 하는 전체 시스템 오버 헤드를 줄여 메모리에 한 번에 반환 하 고 기본적으로 저장 한 행 수를 쿼리 결과 대 한 대기 중인 아니라를 사용할 수 있습니다.  
  
 인스턴스를 만든 후에 **명령** 만들 클래스는 **DataReader** 호출 하 여 개체 **Command.ExecuteReader** 데이터 원본에서 행을 검색 합니다. **DataReader** 구현은 두 가지 기본 기능을 제공 해야: 정방향 전용 액세스는 결과 대해 명령과 열 유형, 이름에 대 한 액세스를 실행 하 여 얻은 설정 하 고 각 행 내에서 값입니다. 클라이언트가 사용 하는 **읽기** 의 메서드는 **DataReader** 개체를 쿼리 결과에서 행을 가져옵니다.  
  
 보고서 디자이너에서 프로그램 **DataReader** 개체와 같은 결과 집합에 대 한 스키마 정보 및 필드 목록을 검색 하는 데 사용 됩니다. 구현 하 여 이렇게는 **GetName**, **GetValue**, **GetFieldType,** 및 **GetOrdinal** 의 메서드는 <xref:Microsoft.ReportingServices.DataProcessing.IDataReader> 인터페이스입니다.  
  
 <xref:Microsoft.ReportingServices.DataProcessing.IDataReaderExtension> 인터페이스를 통해 결과 집합에 대한 특정 집계 정보를 제공할 수 있습니다. 샘플 **DataReader** 클래스 구현, 참조 [SQL Server Reporting Services 제품 샘플](http://go.microsoft.com/fwlink/?LinkId=177889)합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [Reporting Services 확장 프로그램](../../../reporting-services/extensions/reporting-services-extensions.md)   
 [데이터 처리 확장 프로그램 구현](../../../reporting-services/extensions/data-processing/implementing-a-data-processing-extension.md)   
 [Reporting Services 확장 프로그램 라이브러리](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  
