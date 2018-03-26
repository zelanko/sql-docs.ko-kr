---
title: SQL Server 설명서에 기여하는 방법 | Microsoft Docs
ms.date: 03/19/2018
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: ''
ms.component: sql-non-specified
ms.reviewer: ''
ms.suite: sql
ms.custom: ''
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: article
author: rothja
ms.author: jroth
manager: craigg
ms.workload: Active
ms.openlocfilehash: 1885c57cfcf21dcdb877fc4c59b229636b74c137
ms.sourcegitcommit: 0d904c23663cebafc48609671156c5ccd8521315
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/19/2018
---
# <a name="how-to-contribute-to-sql-server-documentation"></a>SQL Server 설명서에 기여하는 방법

[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md.md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

모든 사용자는 SQL Server 설명서에 기여할 수 있습니다. 오타 수정, 더 나은 설명 제안 및 기술적 정확성 향상을 포함합니다. 이 문서는 콘텐츠 참여를 시작하는 방법 및 프로세스 작동 방법을 설명합니다.

참여하기 위해 사용할 수 있는 두 가지 주 워크플로가 있습니다.

|||
|---|---|
| [브라우저에서 편집](#githubui) | 모든 문서의 작고 빠른 편집에 적합합니다. |
| [도구를 사용하여 로컬로 편집](#tools) | 더 복잡한 편집, 여러 문서를 포함하는 편집 및 docs.microsoft.com에 대한 빈번한 참여에 적합합니다. |

## <a id="githubui"></a> 브라우저에서 편집

다음 단계는 브라우저에서 SQL Server 콘텐츠에 대한 간단한 편집을 수행하는 개요를 제공합니다. 전체 프로세스는 문서, [사소하거나 드문 변경 내용에 대한 GitHub 참여 워크플로](https://docs.microsoft.com/contribute/contribute/light-workflow)에 설명되어 있습니다.

1. 이를 포함하는 모든 문서에는 오른쪽에 **편집** 단추가 있습니다. 변경하려는 문서를 찾고, **편집** 단추를 클릭하여 시작합니다.

   ![SQL 문서에 대한 편집 단추](./media/sql-server-docs-contribute/edit-sql-server-docs.png)

   docs.microsoft.com의 모든 콘텐츠는 다양한 GitHub 리포지토리에서 관리됩니다. 편집 단추를 클릭하면 **sql-docs** 리포지토리의 문서로 이동됩니다. 또는 Azure 설명서에서 SQL 문서를 편집하는 경우 **azure-docs** 리포지토리로 이동됩니다. 

1. 다음으로 GitHub에서 문서의 오른쪽 위에 있는 연필 아이콘을 클릭합니다.

   ![편집 단추](./media/sql-server-docs-contribute/edit-button.png)

   > [!NOTE]
   > 문서를 편집하려면 GitHub에 로그인해야 합니다. GitHub 계정이 없는 경우 [GitHub 계정 설정](https://docs.microsoft.com/contribute/contribute/get-started-setup-github)을 참조하세요. 새 계정을 만든 후 편집하려면 GitHub로 이메일 주소를 확인해야 합니다.

1. 브라우저에서 문서를 편집합니다. 모든 문서는 Markdown으로 작성됩니다. 마크다운에서 도움이 필요한 경우 [Markdown 기본 사항](https://help.github.com/articles/getting-started-with-writing-and-formatting-on-github/)을 검토할 수 있습니다. 게시된 문서가 기존 Markdown을 렌더링하는 방법을 관찰하여 배울 수도 있습니다.

1. 편집 창의 맨 아래로 스크롤하고, 변경 내용의 제목을 입력하고, **파일 변경 내용 제안** 단추를 클릭합니다.

   ![끌어오기 요청 제안](./media/sql-server-docs-contribute/propose-file-change.png)

1. 다음 페이지에서 **끌어오기 요청 만들기**를 클릭합니다.

   ![끌어오기 요청 만들기](./media/sql-server-docs-contribute/create-pull-request.png)

1. 끌어오기 요청에 대한 제목과 설명을 입력합니다. 그런 다음, **끌어오기 요청 만들기**를 다시 클릭합니다.

   ![끌어오기 요청 만들기](./media/sql-server-docs-contribute/create-pull-request2.png)

이 시점에서 끌어오기 요청 설명의 나머지 프로세스를 통해 안내해야 합니다. 전체 프로세스 및 추가 세부 정보는[참가자 가이드](https://docs.microsoft.com/contribute/contribute/light-workflow)에서 찾을 수 있습니다.

## <a id="tools"></a> 도구를 사용하여 로컬로 편집

또 다른 편집 옵션은 **sql-docs** 또는 **azure-docs** 리포지토리를 포크하고 컴퓨터에 로컬로 복제하는 것입니다. 그런 다음, Markdown 편집기 및 git 클라이언트를 사용하여 변경 내용을 전송할 수 있습니다. 이 워크플로는 더 복잡하거나 여러 파일을 포함하는 편집에 적합합니다. docs.microsoft.com에 대한 빈번한 참가자에게도 적합합니다.

이 방법을 사용하여 참여하려면 다음 문서를 참조하세요.

- [GitHub 계정 만들기](https://docs.microsoft.com/contribute/contribute/get-started-setup-github)
- [콘텐츠 제작 도구 설치](https://docs.microsoft.com/contribute/contribute/get-started-setup-tools)
- [로컬로 Git 리포지토리 설정](https://docs.microsoft.com/contribute/contribute/get-started-setup-local)
- [도구를 사용하여 참여](https://docs.microsoft.com/contribute/contribute/full-workflow)

설명서에 중요한 변경 내용이 있는 끌어오기 요청을 제출하는 경우 GitHub에서 온라인 **기여 CLA(라이선스 규약)**를 제출하도록 요청하는 메시지를 받습니다. 끌어오기 요청을 수락되도록 하려면 온라인 양식을 완료해야 합니다.

## <a name="recognition"></a>인식

변경 내용이 수락된 경우 문서 맨 위에서 참가자로 인식됩니다.

![콘텐츠 기여 인식](./media/sql-server-docs-contribute/contribution-recognition.png)

## <a name="sql-docs-overview"></a>sql-docs 개요

이 섹션에서는 **sql-docs** 리포지토리에서 사용에 대한 일부 추가 지침을 제공합니다.

> [!IMPORTANT]
> 이 섹션의 정보는 **sql-docs**에 관련된 것입니다. Azure 설명서에서 SQL 문서를 편집하는 경우 [GitHub의 azure-docs 리포지토리에 대한 추가 정보](https://github.com/MicrosoftDocs/azure-docs/blob/master/README.md)를 참조하세요.

[sql-docs](https://github.com/MicrosoftDocs/sql-docs) 리포지토리는 콘텐츠를 구성하기 위해 여러 개의 표준 폴더를 사용합니다.

| Folder | Description |
|---|---|
| [docs](https://github.com/MicrosoftDocs/sql-docs/tree/live/docs) | 게시된 모든 SQL Server 콘텐츠를 포함합니다. 하위 폴더는 논리적으로 다양한 영역의 콘텐츠를 구성합니다. |
| [docs/includes](https://github.com/MicrosoftDocs/sql-docs/tree/live/docs/includes) | include 파일을 포함합니다. 이러한 파일은 하나 이상의 다른 항목에 포함될 수 있는 콘텐츠의 블록입니다. |
| **./media** | 각 폴더는 문서 이미지에 대해 하나의 **미디어** 하위 폴더를 가질 수 있습니다. **미디어** 폴더는 이미지가 나타나는 항목과 동일한 이름이 있는 하위 폴더를 차례로 갖습니다. 이미지는 모두 소문자이며 공백이 없는 .png 파일이어야 합니다. |
| **TOC.MD** | 콘텐츠의 테이블 파일입니다. 각 하위 폴더에는 하나의 TOC.MD 파일을 사용하는 옵션이 있습니다. |

#### <a name="applies-to-includes"></a>Applies-to includes

각 SQL Server 문서는 제목 뒤에 **applies-to** include 파일을 포함합니다. 이는 문서가 적용되는 영역 또는 SQL Server의 버전을 나타냅니다.

**appliesto-ss-asdb-asdw-pdw-md.md** include 파일을 끌어오는 다음 Markdown 예제를 고려합니다.

```Markdown
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
```

문서의 위쪽에 다음 텍스트를 추가합니다.

![Applies to 텍스트](./media/sql-server-docs-contribute/applies-to.png)

문서에 대한 올바른 applies-to include를 찾으려면 다음 팁을 사용합니다.

- 동일한 기능 또는 관련된 작업을 다루는 다른 문서를 살펴봅니다. 해당 문서를 편집하는 경우 applies-to include에 대한 Markdown을 복사할 수 있습니다(제출하지 않고 편집을 취소할 수 있음).
- 텍스트 "applies-to"를 포함하는 파일에 대한 [docs/includes](https://github.com/MicrosoftDocs/sql-docs/tree/live/docs/includes) 디렉터리를 검색합니다. github에서 **찾기** 버튼을 사용하여 신속하게 필터링할 수 있습니다. 파일을 클릭하여 렌더링되는 방법을 확인합니다.
- 명명 규칙에 유의하십시오. 이름에 x가 있는 경우 일반적으로 서비스에 대한 지원 부족을 나타내는 자리 표시자입니다. 예를 들어 **appliesto-xx-xxxx-asdw-xxx-md.md**는 **asdw**만 설명된 반면 다른 필드에는 x가 있으므로 Azure SQL Data Warehouse에 대한 지원만을 나타냅니다.
- 일부 includes는 **tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md**와 같은 버전 번호를 지정합니다. 특정 버전의 SQL Server를 사용하여 도입된 기능을 아는 경우 이러한 includes를 사용합니다. 

## <a name="contributor-resources"></a>참가자 리소스

- [docs.microsoft.com에 대한 참가자 가이드](https://docs.microsoft.com/en-us/contribute/)
- [Microsoft 스타일 가이드](https://docs.microsoft.com/en-us/teamblog/style-guide)
- [Markdown 기본 사항](https://help.github.com/articles/getting-started-with-writing-and-formatting-on-github/)

> [!TIP]
> 설명서 피드백 외에 제품 피드백이 있는 경우 [여기에서 SQL Server 제품에 대한 피드백을 제공합니다](https://feedback.azure.com/forums/908035-sql-server).

## <a name="next-steps"></a>다음 단계

GitHub에서 [sql-docs 리포지토리](https://github.com/MicrosoftDocs/sql-docs)를 탐색합니다.

문서를 찾고, 변경 내용을 전송하고, SQL Server 커뮤니티에 도움을 주세요. 

감사합니다.


