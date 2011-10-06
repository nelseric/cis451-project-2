
# This bash script launches the JLS circuit tester, provided JLS.jar and 
# JLSCircuitTester.jar are in the same directory
# as this file.

# $0 contains the "name" of this script (the command typed at the
# command line to launch it).  The dirname utility takes off the name
# of the file and leaves the name of the directory containing the
# script.  That directory name is then used to tell java where to find
# JLS.

# Notice that "." and $JLSCT_CLASSPATH are in the classpath.  This 
# allows java to find any user-written OutputSets. 

dir=`dirname $0`
#echo "Dirname is " $dir

# Make sure JLS.jar is around.
if [ ! -e $dir/JLS.jar ]
then
	echo "JLS.jar is missing (or not in the right place)."
	exit 1
fi

java -Xmx256m -cp $dir/JLS.jar:$dir/jlsCircuitTester.jar:.:$JLSCT_CLASSPATH -ea edu.gvsu.cis.kurmasz.jls.JLSCircuitTester "$@"
exit $?  # causes the script to have the same exit value as the JVM.
