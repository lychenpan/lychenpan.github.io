title: Custom lombok buider
author: ChenPan
tags:
  - lombok
  - java
  - self-record
  - ''
categories:
  - self-record
date: 2017-11-16 18:09:00
---
Use lombok's annotation will reduce lots of redundant code in java, like getter and setter.<br>
Less talk, show the code

```
@Data
@AllArgsConstructor
@NoArgsConstructor
@Builder
public class JobStatusMessage {
    private String jobID;
    @NonNull
    private String status;
    @NonNull
    private String version;
    private String error;
}
```
In this way, we can construct the data class in a very easy way:

```
JobStatusMessage jobStatusMessage = JobStatusMessage.builder()
				.status("failed")
                .version("18.01")
                .error(ex.getMessage()).build();
```
Builder supply each setter method for each field. But it has limitition. What if we want to setter multi fields in one time. 
<br> We can cutom the builder this way:
```
@Data
@AllArgsConstructor
@NoArgsConstructor
@Builder
public class JobStatusMessage {
    private String jobID;
    @NonNull
    private String status;
    @NonNull
    private String version;
    private String error;
    public static class JobStatusMessageBuilder {
        public JobStatusMessageBuilder success(String jobID, String status, String error) {
            return this.jobID(jobID).status("success").version("18.01").error(error);
        }
    }
}
```
Then u can construct data object more eaiser way:
```
JobStatusMessage jobStatusMessage = JobStatusMessage.builder().success("test","test","test").build();
```
In the same time, filed setter function are still kept.

TODO: why this works??