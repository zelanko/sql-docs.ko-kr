---
title: 샘플 JDBC 드라이버 애플리케이션 | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: e136b87c-a138-45d6-8c3e-bcef94b7e483
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: fd4c3a723cc032a1e14c87abfdc09424a515ac8e
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/08/2020
ms.locfileid: "80922574"
---
# <a name="sample-jdbc-driver-applications"></a>샘플 JDBC 드라이버 애플리케이션

[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] 샘플 애플리케이션은 JDBC 드라이버의 다양한 기능을 보여줍니다. 또한 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터베이스와 함께 JDBC 드라이버를 사용할 때 참고할 수 있는 바람직한 프로그래밍 방식도 보여줍니다.  
  
모든 샘플 애플리케이션은 로컬 컴퓨터에서 컴파일 및 실행된 *.java 코드 파일 형식으로 포함되며 다음 위치에 있는 여러 하위 폴더에 들어 있습니다.  

```bash
\<installation directory>\sqljdbc_<version>\<language>\samples  
```

 이 섹션의 항목에서는 샘플 애플리케이션을 구성 및 실행하는 방법과 함께 샘플 애플리케이션이 소개하는 내용에 대해 설명합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
  
| 항목                                                                                                                  | Description                                                                                                                                                                                                                                                                   |
| ---------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [데이터 연결 및 검색](../../../connect/jdbc/code-samples/connecting-and-retrieving-data.md)                              | 이 샘플 애플리케이션은 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터베이스에 연결하는 방법을 보여줍니다. 또한 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터베이스에서 데이터를 검색하는 다양한 방법도 보여줍니다. |
| [데이터 형식 작업 &#40;JDBC&#41;](../../../connect/jdbc/code-samples/working-with-data-types-jdbc.md)                        | 이 샘플 애플리케이션은 JDBC 드라이버 데이터 형식을 사용하여 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터베이스의 데이터로 작업하는 방법을 보여줍니다.                                                                                              |
| [결과 집합 작업](../../../connect/jdbc/code-samples/working-with-result-sets.md)                                          | 이 샘플 애플리케이션은 결과 집합을 사용하여 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터베이스에 포함된 데이터를 처리하는 방법을 소개합니다.                                                                                                            |
| [대규모 데이터 작업](../../../connect/jdbc/code-samples/working-with-large-data.md)                                            | 이러한 샘플 애플리케이션은 선택 버퍼링을 사용하여 서버 커서 오버헤드 없이 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터베이스에서 큰 값 데이터를 검색하는 방법에 대해 설명합니다.                                                         |
| [SQL 데이터 검색 및 분류](../../jdbc/code-samples/data-discovery-and-classification-sample.md) | 이 샘플 애플리케이션은 JDBC 드라이버를 사용하여 ResultSet 개체에서 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터베이스에 포함된 데이터 검색 및 분류 정보를 검색하는 방법을 보여 줍니다.                                            |
  
## <a name="see-also"></a>참고 항목

[JDBC 드라이버 개요](../../../connect/jdbc/overview-of-the-jdbc-driver.md)
