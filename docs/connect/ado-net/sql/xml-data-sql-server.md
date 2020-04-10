---
title: SQL Server의 XML 데이터
description: SQL Server에서 검색된 XML 데이터를 사용하는 방법을 설명합니다.
ms.date: 08/15/2019
ms.assetid: 9849d319-f518-4e3d-a7cd-f8fdcaaa1d4d
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-kaywon
ms.openlocfilehash: e2d181ce82cfa9d71f2902e3a50e50ed80f0c465
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80918243"
---
# <a name="xml-data-in-sql-server"></a>SQL Server의 XML 데이터

[!INCLUDE[Driver_ADONET_Download](../../../includes/driver_adonet_download.md)]

SQL Server에서는 .NET 내에 SQLXML의 기능을 노출시킵니다. 개발자들은 SQL Server의 인스턴스에서 XML 데이터에 액세스하고 .NET 환경으로 데이터를 가져와서 처리한 후 업데이트를 다시 SQL Server로 보내는 애플리케이션들을 작성할 수 있습니다. SQL Server에서는 데이터 스토리지 및 데이터 검색을 위한 매개 변수 값을 비롯하여 여러 가지 방식으로 XML 데이터를 사용할 수 있습니다. .NET의 **SqlXml** 클래스에서는 SQL Server 내의 XML 열에 저장된 데이터로 작업하기 위한 클라이언트 쪽 지원을 제공합니다. 자세한 내용은 SQL Server 온라인 설명서의 "SQLXML 관리되는 클래스"를 참조하세요.  
  
## <a name="in-this-section"></a>섹션 내용  
[SQL XML 열 값](sql-xml-column-values.md)  
SQL Server에서 XML 데이터를 검색하고 검색한 데이터로 작업하는 방법을 설명합니다.  
  
[XML 값을 매개 변수로 지정](specify-xml-values-parameters.md)  
하나의 명령에 XML 데이터를 매개 변수로서 전달하는 방법을 보여줍니다.  
  
## <a name="next-steps"></a>다음 단계
- [SQL Server 및 ADO.NET](index.md)
