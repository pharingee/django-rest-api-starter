import logging

from django.core.exceptions import ValidationError, ObjectDoesNotExist
from django.http.response import Http404
from rest_framework import status
from rest_framework.response import Response
from rest_framework.exceptions import PermissionDenied


logger = logging.getLogger('django')


def exception_handler(func):
    def execute_and_catch(*args, **kwargs):
        try:
            return func(*args, **kwargs)
        except KeyError, e:
            return Response(
                {'details': str(e) + 'is missing'},
                status=status.HTTP_400_BAD_REQUEST
            )
        except ObjectDoesNotExist, e:
            return Response(
                {'details': str(e)},
                status=status.HTTP_400_BAD_REQUEST
            )
        except Http404, e:
            return Response(
                {'details': str(e)},
                status=status.HTTP_404_NOT_FOUND
            )
        except ValidationError, e:
            return Response(
                {'details': str(e)},
                status=status.HTTP_400_BAD_REQUEST
            )
        except PermissionDenied, e:
            return Response(
                {'details': str(e)},
                status=status.HTTP_400_BAD_REQUEST
            )
        except Exception, e:
            logger.exception(e)
            return Response(
                {'details': 'Oops'},
                status=status.HTTP_500_INTERNAL_SERVER_ERROR
            )

    return execute_and_catch
