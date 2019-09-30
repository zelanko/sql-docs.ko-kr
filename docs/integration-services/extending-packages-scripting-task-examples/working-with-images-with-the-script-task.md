---
title: 스크립트 태스크를 사용한 이미지 작업 | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
helpviewer_keywords:
- graphics [Integration Services]
- Script task [Integration Services], images
- Drawing namespace
- images [Integration Services]
- SSIS Script task, images
- Script task [Integration Services], examples
- thumbnails [Integration Services]
- System.Drawing namespace
- JPEG format [Integration Services]
- .jpeg files
ms.assetid: 74aeb7ab-51b2-4b9f-84ee-0b46a7908ab9
author: chugugrace
ms.author: chugu
ms.openlocfilehash: bed89f0cade880f41122e921fbda146ae2abc28d
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/26/2019
ms.locfileid: "71296974"
---
# <a name="working-with-images-with-the-script-task"></a>스크립트 태스크를 사용한 이미지 작업

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  제품 또는 사용자 데이터베이스에는 텍스트 및 숫자 데이터 외에 이미지도 포함되는 경우가 많습니다. Microsoft .NET Framework의 **System.Drawing** 네임스페이스에서는 이미지 조작을 위한 클래스를 제공합니다.  
  
 [예제 1: JPEG 형식으로 이미지 변환](#example1)  
  
 [예제 2: 썸네일 이미지 만들기 및 저장](#example2)  
  
> [!NOTE]  
>  여러 패키지에서 쉽게 다시 사용할 수 있는 태스크를 만들려면 이 스크립트 태스크 예제에 있는 코드를 바탕으로 사용자 지정 태스크를 만들어 보십시오. 자세한 내용은 [사용자 지정 태스크 개발](../../integration-services/extending-packages-custom-objects/task/developing-a-custom-task.md)을 참조하세요.  
  
##  <a name="example1"></a> 예 1 설명: JPEG 형식으로 이미지 변환  
 다음 예에서는 변수로 지정된 이미지 파일을 열고 인코더를 사용하여 이 파일을 압축된 JPEG 파일로 저장합니다. 인코더 정보를 검색하는 코드는 프라이빗 함수에 캡슐화되어 있습니다.  
  
#### <a name="to-configure-this-script-task-example-for-use-with-a-single-image-file"></a>이 스크립트 태스크 예를 단일 이미지 파일에 사용할 수 있도록 구성하려면  
  
1.  `CurrentImageFile`이라는 문자열 변수를 만들고 해당 값을 기존 이미지 파일의 경로 및 파일 이름으로 설정합니다.  
  
2.  **스크립트 태스크 편집기**의 **스크립트** 페이지에서 **ReadOnlyVariables** 속성에 `CurrentImageFile` 변수를 추가합니다.  
  
3.  스크립트 프로젝트에서 **System.Drawing** 네임스페이스에 대한 참조를 설정합니다.  
  
4.  코드에서 **Imports** 문을 사용하여 **System.Drawing** 및 **System.IO** 네임스페이스를 가져옵니다.  
  
#### <a name="to-configure-this-script-task-example-for-use-with-multiple-image-files"></a>이 스크립트 태스크 예를 여러 이미지 파일에 사용할 수 있도록 구성하려면  
  
1.  Foreach 루프 컨테이너 내에 스크립트 태스크를 추가합니다.  
  
2.  **Foreach 루프 편집기**의 **컬렉션** 페이지에서 열거자로 **Foreach File 열거자**를 선택하고 원본 파일의 경로 및 파일 마스크(예: "*.bmp")를 지정합니다.  
  
3.  **변수 매핑** 페이지에서 `CurrentImageFile` 변수를 인덱스 0으로 매핑합니다. 이 변수는 현재 파일 이름을 열거자의 각 반복에 있는 스크립트 태스크에 전달합니다.  
  
    > [!NOTE]  
    >  이러한 단계는 단일 이미지 파일에 사용하기 위한 절차에 나열된 단계에 추가적으로 수행합니다.  
  
### <a name="example-1-code"></a>예 1 코드  
  
```vb  
Public Sub Main()  
  
    'Create and initialize variables.  
    Dim currentFile As String  
    Dim newFile As String  
    Dim bmp As Bitmap  
    Dim eps As New Imaging.EncoderParameters(1)  
    Dim ici As Imaging.ImageCodecInfo  
    Dim supportedExtensions() As String = _  
        {".BMP", ".GIF", ".JPG", ".JPEG", ".EXIF", ".PNG", _  
        ".TIFF", ".TIF", ".ICO", ".ICON"}  
  
    Try  
        'Store the variable in a string for local manipulation.  
        currentFile = Dts.Variables("CurrentImageFile").Value.ToString  
        'Check the extension of the file against a list of  
        'files that the Bitmap class supports.  
        If Array.IndexOf(supportedExtensions, _  
            Path.GetExtension(currentFile).ToUpper) > -1 Then  
  
            'Load the file.  
            bmp = New Bitmap(currentFile)  
  
            'Calculate the new name for the compressed image.  
            'Note: This will overwrite existing JPEGs.  
            newFile = Path.Combine( _  
                Path.GetDirectoryName(currentFile), _  
                String.Concat(Path.GetFileNameWithoutExtension(currentFile), _  
                ".jpg"))  
  
            'Specify the compression ratio (0=worst quality, 100=best quality).  
            eps.Param(0) = New Imaging.EncoderParameter( _  
                Imaging.Encoder.Quality, 75)  
  
            'Retrieve the ImageCodecInfo associated with the jpeg format.  
            ici = GetEncoderInfo("image/jpeg")  
  
            'Save the file, compressing it into the jpeg encoding.  
            bmp.Save(newFile, ici, eps)  
        Else  
            'The file is not supported by the Bitmap class.  
            Dts.Events.FireWarning(0, "Image Resampling Sample", _  
                "File " & currentFile & " is not a supported format.", _  
                "", 0)  
         End If  
        Dts.TaskResult = ScriptResults.Success  
    Catch ex As Exception  
        'An error occurred.  
        Dts.Events.FireError(0, "Image Resampling Sample", _  
            ex.Message & ControlChars.CrLf & ex.StackTrace, _  
            String.Empty, 0)  
        Dts.TaskResult = ScriptResults.Failure  
    End Try  
  
End Sub  
  
Private Function GetEncoderInfo(ByVal mimeType As String) As Imaging.ImageCodecInfo  
  
    'The available image codecs are returned as an array,  
    'which requires code to iterate until the specified codec is found.  
  
    Dim count As Integer  
    Dim encoders() As Imaging.ImageCodecInfo  
  
    encoders = Imaging.ImageCodecInfo.GetImageEncoders()  
  
    For count = 0 To encoders.Length  
        If encoders(count).MimeType = mimeType Then  
            Return encoders(count)  
        End If  
    Next  
  
    'This point is only reached if a codec is not found.  
    Err.Raise(513, "Image Resampling Sample", String.Format( _  
        "The {0} codec is not available. Unable to compress file.", _  
            mimeType))  
    Return Nothing  
  
End Function  
  
```  
  
##  <a name="example2"></a> 예 2 설명: 썸네일 이미지 만들기 및 저장  
 다음 예에서는 변수로 지정된 이미지 파일을 열고, 가로 세로 비율을 일정하게 유지하면서 이미지의 축소판 그림을 만들고, 이 축소판 그림을 수정된 파일 이름으로 저장합니다. 가로 세로 비율을 일정하게 유지하면서 축소판 그림의 높이와 너비를 계산하는 코드는 프라이빗 서브루틴에 캡슐화되어 있습니다.  
  
#### <a name="to-configure-this-script-task-example-for-use-with-a-single-image-file"></a>이 스크립트 태스크 예를 단일 이미지 파일에 사용할 수 있도록 구성하려면  
  
1.  `CurrentImageFile`이라는 문자열 변수를 만들고 해당 값을 기존 이미지 파일의 경로 및 파일 이름으로 설정합니다.  
  
2.  또한 `MaxThumbSize`라는 정수 변수를 만들고 100과 같이 값을 픽셀 단위로 할당합니다.  
  
3.  **스크립트 태스크 편집기**의 **스크립트** 페이지에서 **ReadOnlyVariables** 속성에 두 변수를 추가합니다.  
  
4.  스크립트 프로젝트에서 **System.Drawing** 네임스페이스에 대한 참조를 설정합니다.  
  
5.  코드에서 **Imports** 문을 사용하여 **System.Drawing** 및 **System.IO** 네임스페이스를 가져옵니다.  
  
#### <a name="to-configure-this-script-task-example-for-use-with-multiple-image-files"></a>이 스크립트 태스크 예를 여러 이미지 파일에 사용할 수 있도록 구성하려면  
  
1.  Foreach 루프 컨테이너 내에 스크립트 태스크를 추가합니다.  
  
2.  **Foreach 루프 편집기**의 **컬렉션** 페이지에서 **열거자**로 **Foreach File 열거자**를 선택하고 원본 파일의 경로 및 파일 마스크(예: "*.jpg")를 지정합니다.  
  
3.  **변수 매핑** 페이지에서 `CurrentImageFile` 변수를 인덱스 0으로 매핑합니다. 이 변수는 현재 파일 이름을 열거자의 각 반복에 있는 스크립트 태스크에 전달합니다.  
  
    > [!NOTE]  
    >  이러한 단계는 단일 이미지 파일에 사용하기 위한 절차에 나열된 단계에 추가적으로 수행합니다.  
  
### <a name="example-2-code"></a>예 2 코드  
  
```vb  
Public Sub Main()  
  
    Dim currentImageFile As String  
    Dim currentImage As Image  
    Dim maxThumbSize As Integer  
    Dim thumbnailImage As Image  
    Dim thumbnailFile As String  
    Dim thumbnailHeight As Integer  
    Dim thumbnailWidth As Integer  
  
    currentImageFile = Dts.Variables("CurrentImageFile").Value.ToString  
    thumbnailFile = Path.Combine( _  
        Path.GetDirectoryName(currentImageFile), _  
        String.Concat(Path.GetFileNameWithoutExtension(currentImageFile), _  
        "_thumbnail.jpg"))  
  
    Try  
        currentImage = Image.FromFile(currentImageFile)  
  
        maxThumbSize = CType(Dts.Variables("MaxThumbSize").Value, Integer)  
        CalculateThumbnailSize( _  
            maxThumbSize, currentImage, thumbnailWidth, thumbnailHeight)  
  
        thumbnailImage = currentImage.GetThumbnailImage( _  
           thumbnailWidth, thumbnailHeight, Nothing, Nothing)  
        thumbnailImage.Save(thumbnailFile)  
        Dts.TaskResult = ScriptResults.Success  
    Catch ex As Exception  
        Dts.Events.FireError(0, "Script Task Example", _  
        ex.Message & ControlChars.CrLf & ex.StackTrace, _  
        String.Empty, 0)  
        Dts.TaskResult = ScriptResults.Failure  
    End Try  
  
End Sub  
  
Private Sub CalculateThumbnailSize( _  
    ByVal maxSize As Integer, ByVal sourceImage As Image, _  
    ByRef thumbWidth As Integer, ByRef thumbHeight As Integer)  
  
    If sourceImage.Width > sourceImage.Height Then  
        thumbWidth = maxSize  
        thumbHeight = CInt((maxSize / sourceImage.Width) * sourceImage.Height)  
    Else  
        thumbHeight = maxSize  
        thumbWidth = CInt((maxSize / sourceImage.Height) * sourceImage.Width)  
    End If  
  
End Sub  
```  
  
```csharp  
bool ThumbnailCallback()  
        {  
            return false;  
        }  
        public void Main()  
        {  
  
            string currentImageFile;  
            Image currentImage;  
            int maxThumbSize;  
            Image thumbnailImage;  
            string thumbnailFile;  
            int thumbnailHeight = 0;  
            int thumbnailWidth = 0;  
  
            currentImageFile = Dts.Variables["CurrentImageFile"].Value.ToString();  
            thumbnailFile = Path.Combine(Path.GetDirectoryName(currentImageFile), String.Concat(Path.GetFileNameWithoutExtension(currentImageFile), "_thumbnail.jpg"));  
  
            try  
            {  
  
                currentImage = Image.FromFile(currentImageFile);  
  
                maxThumbSize = (int)Dts.Variables["MaxThumbSize"].Value;  
                CalculateThumbnailSize(maxThumbSize, currentImage, ref thumbnailWidth, ref thumbnailHeight);  
  
                Image.GetThumbnailImageAbort myCallback = new Image.GetThumbnailImageAbort(ThumbnailCallback);  
  
                thumbnailImage = currentImage.GetThumbnailImage(thumbnailWidth, thumbnailHeight, ThumbnailCallback, IntPtr.Zero);  
                thumbnailImage.Save(thumbnailFile);  
                Dts.TaskResult = (int)ScriptResults.Success;  
            }  
            catch (Exception ex)  
            {  
                Dts.Events.FireError(0, "Script Task Example", ex.Message + "\r" + ex.StackTrace, String.Empty, 0);  
                Dts.TaskResult = (int)ScriptResults.Failure;  
            }  
  
        }  
  
        private void CalculateThumbnailSize(int maxSize, Image sourceImage, ref int thumbWidth, ref int thumbHeight)  
        {  
  
            if (sourceImage.Width > sourceImage.Height)  
            {  
                thumbWidth = maxSize;  
                thumbHeight = (int)(sourceImage.Height * maxSize / sourceImage.Width);  
            }  
            else  
            {  
                thumbHeight = maxSize;  
                thumbWidth = (int)(sourceImage.Width * maxSize / sourceImage.Height);  
  
            }  
  
        }  
  
```  
  
  
