<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Форма загрузки документов и панель администратора</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f0f2f5;
            color: #333;
            margin: 0;
            padding: 0;
        }
        h2 {
            color: #4a90e2;
            text-align: center;
        }
        h3 {
            color: #333;
            font-size: 1.2em;
            margin-bottom: 10px;
        }
        form, .admin-panel {
            max-width: 500px;
            margin: 20px auto;
            padding: 20px;
            background-color: #fff;
            border: 1px solid #ddd;
            border-radius: 8px;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
        }
        label {
            display: block;
            font-weight: bold;
            margin-bottom: 5px;
            color: #333;
        }
        input[type="text"], input[type="file"] {
            width: 100%;
            padding: 10px;
            margin-bottom: 15px;
            border: 1px solid #ddd;
            border-radius: 5px;
            box-sizing: border-box;
        }
        button {
            display: inline-block;
            background-color: #4a90e2;
            color: #fff;
            padding: 10px 20px;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            font-size: 1em;
            transition: background-color 0.3s ease;
            width: 100%;
        }
        button:hover {
            background-color: #357ab8;
        }
        .admin-panel {
            display: none;
            padding-top: 0;
        }
        .file-info {
            margin: 10px 0;
            padding: 15px;
            background-color: #e9f4ff;
            border: 1px solid #4a90e2;
            border-radius: 5px;
        }
        .file-info strong {
            color: #333;
        }
        .no-files {
            color: #999;
            text-align: center;
        }
    </style>
</head>
<body>

<h2>Форма загрузки документов</h2>
<form id="uploadForm">
    <label for="name">Имя:</label>
    <input type="text" name="name" id="name" required>

    <label for="imageLink">Ссылка на изображение (Imgur/Yapix):</label>
    <input type="text" name="imageLink" id="imageLink" placeholder="Введите ссылку на изображение" required>

    <label for="file">Выберите файл для загрузки:</label>
    <input type="file" name="file" id="file" required>

    <button type="button" onclick="uploadFile()">Загрузить</button>
</form>

<h2>Панель администратора</h2>
<div class="admin-panel" id="adminPanel">
    <h3>Загруженные файлы:</h3>
    <div id="uploadedFiles" class="no-files">
        <p>Нет загруженных файлов.</p>
    </div>
</div>

<script>
    const isAdmin = true;

    window.onload = function() {
        if (isAdmin) {
            document.getElementById("adminPanel").style.display = "block";
        }
    }

    function uploadFile() {
        const name = document.getElementById("name").value;
        const imageLink = document.getElementById("imageLink").value;
        const fileInput = document.getElementById("file");

        if (fileInput.files.length === 0) {
            alert("Выберите файл для загрузки.");
            return;
        }

        const file = fileInput.files[0];
        const fileName = file.name;

        if (isAdmin) {
            const uploadedFilesDiv = document.getElementById("uploadedFiles");
            const fileInfo = document.createElement("div");
            fileInfo.className = "file-info";
            fileInfo.innerHTML = `<strong>Имя:</strong> ${name} <br> <strong>Ссылка на изображение:</strong> <a href="${imageLink}" target="_blank">${imageLink}</a> <br> <strong>Файл:</strong> ${fileName}`;

            if (uploadedFilesDiv.classList.contains("no-files")) {
                uploadedFilesDiv.innerHTML = "";
                uploadedFilesDiv.classList.remove("no-files");
            }
            uploadedFilesDiv.appendChild(fileInfo);
        } else {
            alert("Только администраторы могут загружать файлы.");
        }

        document.getElementById("uploadForm").reset();
    }
</script>

</body>
</html>
