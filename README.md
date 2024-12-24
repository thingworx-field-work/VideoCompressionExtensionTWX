# Video Compression Extension for Thingworx

This is a thingworx sdk extension that uses [ffmpeg](https://www.ffmpeg.org/) to compress video.

## Usage

### Initialization
1. Create a new thing using the `VideoConversionThingTemplate` template.
2. Go to configuration and provide the path to the folder with the ffmpeg binary
3. Provide the ffmpeg arguments that are used when user doesn't specify custom ones
4. Test the configuration by running the `GetFFmpegVersion` service.

### Runtime usage

Using the thing created above is quite simple. Only once conversion happens at a time. Two services are of importance:
* `AddVideoProcessingJob`: Creates a new processing job and add it to the queue. The service returns a infotable row with the job id. The following parameters are needed
    * `sourceFileRepo` - File repository where the file to convert is
    * `sourceFilePath` - Path to the file to convert
    * `targetFileRepo` - File repository where to store the converted file
    * `targetFilePath` - Path to the file to converted
    * `arguments`      - If provided, the arguments that are passed to ffmpeg for conversion. If not provided, the ones in the configuration are used.
* `CancelProcessingJob`:  Cancels a job, if queued or running.
    * `jobId`          - Job to cancel
    
When a job is completed, two events can trigger and be subscribed:
* `ProcessingFinished`: a job has finished, and the conversion was successful.
* `ProcessingFailed`: a job has finished but has thrown an error. The `message` column contains information about why it failed.

The `ProcessingQueue` property contains information about the jobs that have completed, are in queue, or are being processed.


#This Extension is provided as-is and without warranty or support. It is not part of the PTC product suite. This project is licensed under the terms of the MIT license  

# Disclaimer
By downloading this software, the user acknowledges that it is unsupported, not reviewed for security purposes, and that the user assumes all risk for running it.

Users accept all risk whatsoever regarding the security of the code they download.

This software is not an official PTC product and is not officially supported by PTC.

PTC is not responsible for any maintenance for this software.

PTC will not accept technical support cases logged related to this Software.

This source code is offered freely and AS IS without any warranty.

The author of this code cannot be held accountable for the well-functioning of it.

The author shared the code that worked at a specific moment in time using specific versions of PTC products at that time, without the intention to make the code compliant with past, current or future versions of those PTC products.

The author has not committed to maintain this code and he may not be bound to maintain or fix it.


# License
I accept the MIT License (https://opensource.org/licenses/MIT) and agree that any software downloaded/utilized will be in compliance with that Agreement. However, despite anything to the contrary in the License Agreement, I agree as follows:

I acknowledge that I am not entitled to support assistance with respect to the software, and PTC will have no obligation to maintain the software or provide bug fixes or security patches or new releases.

The software is provided “As Is” and with no warranty, indemnitees or guarantees whatsoever, and PTC will have no liability whatsoever with respect to the software, including with respect to any intellectual property infringement claims or security incidents or data loss.
