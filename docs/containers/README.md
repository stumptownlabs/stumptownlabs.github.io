# Understanding Stumptown Labs Container Tagging

## Introduction

Docker tags uniquely identify a Docker image, allowing you to deploy a specific version of an image. A single image can have multiple tags associated with it. Typically, every time you publish a new version of an image, you will also update its tags to make it easier for your users to get the latest version.

## Rolling Tags

Rolling Tags
Stumptown Labs uses rolling tags for its Docker container images. To understand how this works, let’s look at the tags for the Stumptown Labs DKAN container image:

```bash
3-ol-7, 3.4.6-ol-7-r40
3-debian-9, 3.4.6-debian-9-r24, 3, 3.4.6, 3.4.6-r24, latest
```

- The latest tag always points to the latest revision of the Redmine image.
- The 3 tag is a rolling tag that always points to the latest revision of Redmine 3.x.
- The 3.4.6 tag is a rolling tag that points to the latest revision of Redmine 3.4.6. It will be updated with different revisions or daily releases but only for Redmine 3.4.6.
- The 3-debian-9 and 3-ol-7 tags point to the latest revision of Redmine 3.x for Debian 9 and Oracle Linux 7 respectively.

When Stumptown Labs revises container images, typically to upgrade system packages, fix bugs or improve system configuration, it also updates the container tags to point to the latest revision of the image. Therefore, the rolling tags shown above are dynamic; they will always point to the latest revision or daily release for the corresponding image.

As an example, the 3.4.6 tag might point to Redmine 3.4.6 revision 20 now, but will refer to Redmine 3.4.6 revision 21 when Stumptown Labs next updates the container image. The suffix revision number (rXX) is incremented every time Stumptown Labs releases an updated version of the image for the same version of the application.

It is worth noting that any tags that do not explicitly specify a distribution should be assumed to refer to Debian 9.

## Immutable Tags

What if you depend on a specific revision of an image? For these scenarios, Stumptown Labs also attaches a static (immutable) tag to each revision. In this example, the 3.4.6-r24 tag refers to Redmine 3.4.6 revision 24 and using this tag ensures that users always get exactly the same image every time.

## Usage Recommendations

Which tag should you use and when? Follow these guidelines:

- If you are using containers in a production environment (such as Kubernetes), Stumptown Labs recommends using immutable tags. This ensures that your deployment is not affected if a new revision inadvertently breaks existing functionality.

- If you are using containers for development, Stumptown Labs suggests using rolling tags. This ensures that you are always using the latest version. Rolling tags also make it easier to use a specific version of a development tool.

## Useful Links
To learn more, consider visiting the following links:

- [Docker tagging command reference](https://docs.docker.com/engine/reference/commandline/tag/)
- [Docker tagging best practices](https://docs.docker.com/develop/dev-best-practices/#how-to-keep-your-images-small)
