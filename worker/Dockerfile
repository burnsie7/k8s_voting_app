FROM microsoft/dotnet:2.0.0-sdk

WORKDIR /code

ADD src/Worker /code/src/Worker

ENV CORECLR_ENABLE_PROFILING=1
ENV CORECLR_PROFILER={846F5F1C-F9AE-4B07-969E-05C26BC060D8}
ENV CORECLR_PROFILER_PATH=/opt/datadog/Datadog.Trace.ClrProfiler.Native.so
ENV DD_INTEGRATIONS=/opt/datadog/integrations.json
ENV DD_DOTNET_TRACER_HOME=/opt/datadog

RUN curl -LO https://github.com/DataDog/dd-trace-dotnet/releases/download/v1.11.0/datadog-dotnet-apm_1.11.0_amd64.deb \
    && dpkg -i ./datadog-dotnet-apm_1.11.0_amd64.deb \ 
    && dotnet restore -v minimal src/Worker \
    && dotnet publish -c Release -o "./" "src/Worker/" 

CMD dotnet src/Worker/Worker.dll
