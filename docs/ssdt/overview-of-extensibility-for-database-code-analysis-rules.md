---
title: 데이터베이스 코드 분석 규칙의 확장성 개요 | Microsoft Docs
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 62f5c980-18d5-43fe-b443-c9e149d01fc7
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 42896bb62b5566c955c86c43618a8f64e4968b5a
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/27/2018
ms.locfileid: "52405870"
---
# <a name="overview-of-extensibility-for-database-code-analysis-rules"></a>데이터베이스 코드 분석 규칙의 확장성 개요
SQL Server Data Tools가 포함된 Visual Studio 버전에는 데이터베이스 코드의 Transact\-SQL 디자인, 명명 및 성능 경고에 대해 보고하는 코드 분석 규칙이 포함되어 있습니다. 자세한 내용은 [데이터베이스 코드를 분석하여 코드 품질 향상](https://msdn.microsoft.com/library/dd172133(v=vs.100).aspx)을 참조하세요.  
  
포함하려는 특정 Transact\-SQL 문제에 대한 처리가 기본 제공 코드 분석 규칙에 포함되지 않은 경우 사용자 지정 데이터베이스 코드 분석 규칙을 만들 수 있습니다. 예를 들어 [SQL Server의 사용자 지정 정적 코드 분석 규칙 어셈블리 작성 연습](../ssdt/walkthrough-author-custom-static-code-analysis-rule-assembly.md)에 나와 있듯이 WAITFOR DELAY 문의 사용을 방지하는 사용자 지정 규칙을 만들 수 있습니다. 사용자 지정 데이터베이스 코드 분석 규칙을 만들려면 [CodeAnalysis](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.codeanalysis.aspx) 네임스페이스의 클래스를 사용합니다.  
  
사용자 지정 코드 분석 규칙을 만들려면 먼저 데이터베이스 코드 분석 규칙의 다양한 구성 요소에 대한 기본적인 아키텍처를 이해해야 합니다.  
  
## <a name="database-code-analysis-rules-components"></a>데이터베이스 코드 분석 규칙 구성 요소  
다음 다이어그램에서는 데이터베이스 코드 분석 규칙 구성 요소가 상호 작용하는 방식을 보여 줍니다.  
  
![데이터베이스 코드 분석 규칙 구성 요소](../ssdt/media/ssdt-database-code-analysis-rules-components.jpg "데이터베이스 코드 분석 규칙 구성 요소")  
  
정적 코드 분석을 직접 실행하거나(자세한 내용은 [방법: Transact-SQL 코드를 분석하여 오류 찾기](https://msdn.microsoft.com/library/dd172119(v=vs.100).aspx) 참조) 빌드를 수행하여 데이터베이스 코드 분석 규칙 기능을 사용하는 경우 프로젝트에서 규칙을 구성한 방식에 따라 모든 규칙이 로드되고 사용됩니다. 자세한 내용은 [방법: 데이터베이스 코드의 정적 분석에 대한 특정 규칙 활성화 및 비활성화](https://msdn.microsoft.com/library/dd172131(v=vs.100).aspx)를 참조하세요. 확장 관리자는 만들고 등록한 모든 사용자 지정 규칙 어셈블리도 로드합니다. 자세한 내용은 [방법: 기능 확장 설치 및 관리](../ssdt/how-to-install-and-manage-feature-extensions.md)를 참조하세요.  
  
사용자 지정 코드 분석 규칙 클래스는 [SqlCodeAnalysisRule](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.codeanalysis.sqlcodeanalysisrule.aspx)에서 상속합니다. 사용자 지정 규칙 클래스는 규칙 실행 컨텍스트를 통해 다양한 유용한 개체에 액세스할 수 있습니다. 이러한 개체는 다음과 같습니다.  
  
-   규칙 자체에 대한 메타데이터  
  
-   모든 모델 요소, 요소 간 관계 및 요소의 속성을 비롯한 데이터베이스의 스키마를 나타내는 Dac.Model.TSqlModel  
  
-   특정 요소를 검사하는 규칙의 경우 모델에서 해당 스키마 요소를 나타내는 Dac.Model.TSqlObject가 컨텍스트에 포함됩니다.  
  
-   많은 스키마 개체에는 이 컨텍스트를 통해 액세스할 수 있는 [ScriptDom](https://msdn.microsoft.com/library/microsoft.sqlserver.transactsql.scriptdom.aspx) 표현도 있습니다. 이 표현은 [SelectStarExpression](https://msdn.microsoft.com/library/microsoft.sqlserver.transactsql.scriptdom.selectstarexpression.aspx)의 존재와 같은 잠재적인 구문 문제를 확인하려는 경우 유용할 수 있는 요소의 AST 기반 표현입니다.  
  
Dac.CodeAnalysis.SqlRuleProblem은 규칙을 통해 발견된 문제를 나타내기 위해 해당 규칙에 따라 만들어집니다. 이 클래스를 만들 때 관련된 Dac.Model.TSqlObject 및 경우에 따라 [ScriptDom](https://msdn.microsoft.com/library/microsoft.sqlserver.transactsql.scriptdom.aspx) 표현 요소가 생성자에 전달되고 소스 코드 파일에서 문제의 위치를 확인하는 데 사용됩니다. 분석이 끝날 때 이러한 모든 문제가 오류 관리자에 전달되며 오류 목록에 표시됩니다.  
  
## <a name="see-also"></a>참고 항목  
[데이터베이스 기능 확장](../ssdt/extending-the-database-features.md)  
  
