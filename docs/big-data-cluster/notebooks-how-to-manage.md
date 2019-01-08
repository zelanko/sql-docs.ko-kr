---
title: Azure Data Studio에 노트북 관리
titleSuffix: SQL Server 2019 big data clusters
description: Azure Data Studio에서 notebook을 관리 하는 방법에 알아봅니다. 여기에 열기, 노트북, 저장 및 빅 데이터 클러스터 연결을 변경 합니다.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 12/06/2018
ms.topic: conceptual
ms.prod: sql
ms.custom: seodec18
ms.openlocfilehash: 998692f56f75e890ef0b4f8e40e256f2ebbd54de
ms.sourcegitcommit: edf7372cb674179f03a330de5e674824a8b4118f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/11/2018
ms.locfileid: "53246592"
---
# <a name="how-to-manage-notebooks-in-azure-data-studio"></a>Azure Data Studio에서 notebook을 관리 하는 방법

이 문서를 열고 SQL Server 2019 미리 보기를 사용 하 여 Azure Data Studio에서 notebook 파일을 저장 하는 방법을 보여 줍니다. 또한 SQL Server 빅 데이터 클러스터에 대 한 연결을 변경 하는 방법을 보여 줍니다.

## <a name="prerequisites"></a>사전 요구 사항

이 문서에서는 Azure Data Studio에서 사용 하려는 노트북을 이미가지고 있다고 가정 합니다. Notebook을 만들려는 경우 참조 [SQL Server 2019 미리 보기에서 notebook을 사용 하는 방법을](notebooks-guidance.md)합니다. Azure Data Studio에서 notebook을 사용 하려면 다음 필수 구성 요소를 충족 해야 합니다.

- [빅 데이터 클러스터를 배포](quickstart-big-data-cluster-deploy.md)합니다.
- [SQL Server 2019 빅 데이터 도구도](deploy-big-data-tools.md):
   - **Azure Data Studio**
   - **SQL Server 2019 확장**
   - **Kubectl**

## <a name="open-a-notebook"></a>Notebook을 엽니다.

여는 방법은 여러 가지는 **노트북 열기** 대화 합니다. 파일 메뉴, 대시보드 및 명령 팔레트를 사용할 수 있습니다. 다음 섹션에서는 각 메서드에 대해 설명합니다.

### <a name="file-menu"></a>파일 메뉴

선택 **파일 열기** 파일 메뉴에서 (Windows)에서 Ctrl + O 및 Cmd + O (Mac)에 있습니다.

![파일 열기를 선택 하 여 파일 열기 대화 상자를 엽니다.](./media/notebooks-how-to-manage/open-file-1.png) 

### <a name="dashboard"></a>대시보드

클릭 **노트북 열기** 대시보드에서 파일 열기 대화 상자를 엽니다.

![대시보드에서 전자 필기장 열기를 선택 하 여 파일 열기 대화 상자를 엽니다.](./media/notebooks-how-to-manage/open-file-2.png) 

### <a name="command-palette"></a>명령 팔레트

명령을 사용 하 여 **파일: 열기** Ctrl + Shift + P (Windows)에서 및 Cmd + Shift + P (Mac)에 입력 하 여 명령 팔레트에서.

![명령 팔레트에서 File:Open를 입력 하 여 파일 열기 대화 상자를 엽니다.](./media/notebooks-how-to-manage/open-file-3.png)

## <a name="save-a-notebook"></a>Notebook을 저장 합니다.

Notebook을 저장 하는 한 가지 방법은 현재 됩니다. 선택 해야 합니다 **저장할** notebook 도구 모음에서 합니다.

![Notebook 도구 모음에서 저장을 클릭 하 여 파일을 저장 합니다.](./media/notebooks-how-to-manage/save-file-1.png)

> [!NOTE]
> 현재 다음 방법 notebook에 변경 내용을 저장 하지 않습니다.
>
> - **파일 저장**, **파일 다른 이름으로 저장 하는 중...**  하 고 **모두 파일 저장** 파일 메뉴에서 명령을 합니다.
> - **파일: 저장** 명령 팔레트에서 입력 된 명령입니다.

## <a name="change-the-big-data-cluster"></a>빅 데이터 클러스터 변경

Notebook에 대 한 SQL Server 빅 데이터 클러스터의 이름을 바꾸려면:

1. 클릭 합니다 **연결할** notebook 도구 모음에서 메뉴.

   ![Notebook 도구 모음에서 메뉴에 연결을 클릭 합니다.](./media/notebooks-how-to-manage/select-attach-to-1.png)

2. 서버를 클릭 합니다 **연결할** 메뉴.

   ![메뉴에는 연결에서 서버 선택](./media/notebooks-how-to-manage/select-attach-to-2.png)

## <a name="next-steps"></a>다음 단계

Azure Data Studio에 노트북에 대 한 자세한 내용은 참조 하세요. [SQL Server 2019 미리 보기에서 notebook을 사용 하는 방법을](notebooks-guidance.md)합니다.