---
title: 데이터 처리 확장 프로그램에 대한 DataReader 클래스 구현 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.topic: reference
helpviewer_keywords:
- data processing extensions [Reporting Services], data readers
- data readers [Reporting Services]
- DataReader class
- read-only data
ms.assetid: 23e286e7-6074-4fbe-be29-203420d6c3d0
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: ff4ba3966523f05d9993df4af616048a16292ea4
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48091913"
---
# <a name="implementing-a-datareader-class-for-a-data-processing-extension"></a>데이터 처리 확장 프로그램에 대한 DataReader 클래스 구현
  **DataReader** 개체가 있으면 클라이언트에서는 읽기 전용, 정방향 전용 데이터 스트림을 데이터 원본에서 검색할 수 있습니다. 결과는 쿼리 실행으로 반환되고 **DataReader** 클래스의 **Read** 메서드를 사용하여 요청할 때까지 클라이언트의 네트워크 버퍼에 저장됩니다. **DataReader** 클래스를 만들려면 <xref:Microsoft.ReportingServices.DataProcessing.IDataReader>를 구현하고 선택적으로 <xref:Microsoft.ReportingServices.DataProcessing.IDataReaderExtension>을 구현합니다. **DataReader** 개체를 사용하면 전체 쿼리 결과가 반환될 때까지 기다리지 않고 사용 가능할 때 즉시 데이터를 검색하고 (기본적으로) 한 번에 행 한 개씩만 메모리에 저장하여 시스템 오버헤드를 줄임으로써 응용 프로그램 성능이 높아집니다.  
  
 **Command** 클래스 인스턴스를 만든 후 **Command.ExecuteReader** 호출을 통해 데이터 원본에서 행을 검색하여 **DataReader** 개체를 만듭니다. **DataReader** 구현은 두 가지 기본적인 기능을 제공해야 하며, 이 두 가지 기능은 명령 실행에서 얻은 결과 집합에 대한 정방향 전용 액세스 기능과 각 행 내의 열 유형, 이름, 값에 대한 액세스 기능입니다. 클라이언트는 **DataReader** 개체의 **Read** 메서드를 사용하여 쿼리 결과에서 행을 얻습니다.  
  
 보고서 디자이너에서 **DataReader** 개체는 결과 집합에 대한 스키마 정보 및 필드 목록을 검색하는 데 사용됩니다. <xref:Microsoft.ReportingServices.DataProcessing.IDataReader> 인터페이스의 **GetName**, **GetValue**, **GetFieldType,** 및 **GetOrdinal** 메서드를 구현하여 이 작업을 수행할 수 있습니다.  
  
 <xref:Microsoft.ReportingServices.DataProcessing.IDataReaderExtension> 인터페이스를 통해 결과 집합에 대한 특정 집계 정보를 제공할 수 있습니다. 예제 **DataReader** 클래스 구현은 [SQL Server Reporting Services 제품 예제](http://go.microsoft.com/fwlink/?LinkId=177889)를 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [Reporting Services 확장 프로그램](../reporting-services-extensions.md)   
 [데이터 처리 확장 프로그램 구현](implementing-a-data-processing-extension.md)   
 [Reporting Services 확장 라이브러리](../reporting-services-extension-library.md)  
  
  
