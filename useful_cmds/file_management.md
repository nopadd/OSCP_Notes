# File\_Management

## Finding Programs

```text
which [command]
```

* Show directory that the executable code is located.

  ```text
  type [file / command]
  ```

* Query the type of the command \(discrete executable or a built-in shell command\).

## Creating Files

```text
echo [data] > [new file].txt
```

* Create a new file.

  ```text
  echo [data] >> [existing file].txt
  ```

* Append data to an existing file.

## Finding Files

```text
find [directory] [criteria option] [text]
```

* Searches within a predefined directory with the criteria option for the given text.

  ```text
  grep [criteria expression] [files]
  ```

* Searches the contents of files and extracts lines matching the criteria expression.
* -r: Enables recursive search on all files contained in the directory.

## Cron Jobs

* Allows users to schedule tasks automatically to run at a specified time and/or date.
* Several files in the /etc/ directory relate to cron jobs: 
  * Cron.daily/hourly/weekly/monthly: Scripts included in each of these folders will automatically run on the specified times of the folder name.
  * Crontab: The cron configuration file that specifies which scripts run at what times under what user permissions. Note that '\*' indicates no value for that column.

